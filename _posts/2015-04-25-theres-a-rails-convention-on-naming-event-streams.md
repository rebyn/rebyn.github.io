---
layout: post
title: There's a Rails' convention on naming event streams
---

In a recent code review, my colleague pointed out that Rails has a convention on naming event streams (`s/streams/(topics|queue_names)/`). It was written at the end of the `ActiveSupport` instrumentation [doco](http://edgeguides.rubyonrails.org/active_support_instrumentation.html#creating-custom-events) quite modestly:

> You should follow Rails conventions when defining your own events. The format is: `event.library`. If you application is sending Tweets, you should create an event named `tweet.twitter`.

My initial thought on this was I felt uneasy doing so, because prefixing event with its namespace/entity/scope sounds like a sure thing to me, ie:

- `billing.invoice_contacts` / `billing.new_customer`; or
- `provisioning.new_instance` / `provisioning.new_instance_ssh_key`

Until I realize I've been doing this all wrong ಠ_ಠ.

This made me take another look at the event payload I sent along, which at the time looked like this:

```
# billing.invoice_contacts
{
  :action => :create,
  :contact_id => an_instance_of(Fixnum)
}
```

I was mixing the event payload, which is supposed to contain states, with the very action that acts upon these states. What's wrong about this approach?

1. I need to reference `payload` to know what to do with that `payload`
2. For Rails' `instrument`/`subscribe`, `payload` can be referenced easily as it's a hash all the way from `instrument` to `subscribe`. However, this introduces unnecessary steps when it comes to using external queues (ie: RabbitMQ, Beanstalkd, etc) where I need to serialize the payload and deserialize it upon receipt.

Then I figure out event streams should be named following the `action_on_things.namespace` format (which Rails is also advocating) to keep me and other developers from being bitten by (1) and (2).

So now these streams are named like:

```
create_invoice_contact.billing
create_customer.billing
create_instance.provisioning
add_shh_key_to_instance.provisioning
```

Mucha better!

===

**Update**:

After a long shower (the only place and time where/when I actually think), I figured out:

3. the Rails convention has nothing to do with naming the event following this format: `action_on_things`
4. `event.library` is still a mystery to me. Given Rails structures resource operations after `Resource#action`, I'm dying to know why they're doing events this way

### `action_on_things`

This works well in the Rails context, where you can select queues using regex with `ActiveSupport::Notification.subscribe` and do (allthenastythings) with those messages in one `subscribe` block. For external queues, I can't imagime myself going through a list of topics to fetch all the relevant messages; not to mention, this's ensured to be horrific with operations that need to be FIFO.