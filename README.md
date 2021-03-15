## Lecture 2 ~ __RPC__

### Motivation for RPC
In distributed systems, software written on different
systems _work together towards a cohesive goal_ (as 
opposed to software that works on a __single system__). 
The different nodes (or systems) need to exchange
messages between each other to interact, and this 
messaging takes place on the network.

Consider, code to process a payment on an e-commerce
application.

```
user = purchasingUser()
card = new Card(user.card.info)

result = paymentService.processPayment(card, 3.99$)
if (result.ok()):
  fulfillOrder()
```
The implementation of processPayment exists on another
system, so a network message needs to be sent with the 
arguments and consequently a network message needs to
be recieved and parsed, which contains the response
to the message (in this case, the result of the payment)
__RPC__ abstracts this underlying networking away, making the
'network function call' similar in use to a local function 
call.

Examples ~ gRPC (Google), Thrift (Facebook), REST, GraphQL(?)

### RPC Client-Server flow

- client invokes the RPC method (RPC stub call)
- RPC client takes __args__ and encodes to a format
ready to be sent over the network (_marshaling_) 
to the RPC server
- RPC server receives call, evaluates function 
results, and marshals result back to RPC client
- RPC client unmarshals results, which are then
available for use on client side
(INSERT IMAGE of marshaling)

Note that RPC __abstracts__ the location of the
resource (function), so this is called __Location
Transparency__
BUT (what if?)
- service crashes during call
- message is lost/delayed
- when is it safe to retry? (things like payments
need to be handled carefully)

### Enterprise Systems and RPC

Sometimes, we want to split a large software 
application into its simpler constituent parts, 
which communicate via RPC. This is often called 
a __Service Oriented Architecture__ or the
__Microservices Approach__

Now, different services can be implemented in
different languages, but they still need to 
interact in a consistent and general fashion. 
Thus for _interoperability_ amongst such services,
we need data type conversions from one language
to the other.

An _interface definition language_(IDL) defines
a language __independent__ API specification
For example, Protocol Buffer is the IDL for gRPC

(INSERT IDL example picture)



