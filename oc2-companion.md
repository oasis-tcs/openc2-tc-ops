# OpenC2 Companion Guide (10 min read)

So, you're curious about [Open Command and Control
(OpenC2)](https://openc2.org/index.html). You've read *most of*
the [OpenC2
specs](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2#technical).
Maybe you've written a quick Consumer to try out. Or maybe you've
done none of those things, but are still curious. What next?

Here is an informal guide to the nitty-gritty of OpenC2.

- [Basics](#basics)
- [OpenC2 Structure](#openc2-structure)
- [Producers and Consumers](#producers-and-consumers)
- [Message: Request or Response](#message-request-or-response)
- [Message: Headers](#message-headers)
- [Command: Action/Target Pair](#command-actiontarget-pair)
- [Actuators](#actuators)
- [Actuator Profiles](#actuator-profiles)
- [Command: Actuator Field](#command-actuator-field)
- [Command ID vs Request ID](#command-id-vs-request-id)
- [Query Features](#query-features)
- [Acknowledgement](#acknowledgement)


# Basics

Before jumping into a lot of text, it will help to see the basic
format of Requests and Responses:

**Example Request in JSON**
```
    "action"     : "deny"
    "target"     : {"ipv4_net" : ["192.168.1.0/24"] }
    
(optional)
    "actuator"   : {"slpf": {} }
    "args"       : {"response_requested" : "ack", "start_time" : 1534775460000 }
    "command_id" : "12345"
```

**Example Response in JSON**
```
    "status"      : 200
    
(optional)
    "status_text" : "The command succeeded"
    "results"     : {"slpf" : {"rule_number": 1234}, "versions" : ["1.0"]}
```

**Example Message Headers in HTTP**
```
Content-type: application/openc2+json;version=1.0
```

 
# OpenC2 Structure

In the above examples, notice how they're all qualified with
*"... in JSON"* or *"... in HTTP"*? Why is that? Why not just say
"Example Request" or "Message Header" without the qualification?

Well, this is both the POWER and the BARRIER-TO-ENTRY of OpenC2.

In reading the specs, you won't find anything like this:

> `The Producer POSTS a JSON "deny" command over TLS to the
> Gateway on port 99, and expects a 200 OK Payload in an HTTP
> Response on success.`
     
Instead, everything in the OpenC2 Language related to Transfer
Protocol, Serialization, Commands and even Device is abstractly
defined or referenced in the [OpenC2 Language Specification
(LS)](https://docs.oasis-open.org/openc2/oc2ls/v1.0/cs02/oc2ls-v1.0-cs02.html).
Then their specific implementations are given in a growing list
of individual specifications. 

This way a system of Producers and Consumers could be
OpenC2-compliant no matter if they're using HTTPS, MQTT, JSON,
CBOR, running on a VM, Mac-Mini, Raspberry Pi, physical router,
etc. The specific Transfer, Serialization, and set of Commands
are composed together with their own specs, and OpenC2 doesn't
prescribe what they run on.

### BECAUSE OF THIS, YOU WILL OFTEN FEEL LIKE YOU'RE MISSING CONCRETE DEFINITIONS OF WHAT OPENC2 IS.

You will never find one document
that tells you everything you need (although the forthcoming
[Architecture
Specification](https://github.com/oasis-tcs/oc2arch/tree/working)
is intended to help with that). Instead, you need to know your
Transfer, Serialization, and Commands ahead of time, then compose
it all yourself. If you are familiar with abstract interfaces in
software development, you might feel right at home reading the
OpenC2 Language spec.

**Composing your Implementation**

```
  OpenC2 Specifications          Other Specifications                       Your Implementation
    |               |                     |
    v               v                     v                               +---------------------+
                                                                          |      Producer(s)    |
                                                                          +---------------------+
+--------+      +--------+                                                   |               ^
|Language|      |Transfer|                                                   |               |
|        |----> | * HTTP |-------------------------------------------------> |               |
|        |      | * MQTT |                                                   |               |
|        |      +--------+                                                   |               |
|        |                                                                   |
|        |      +--------+                                                   |           "status": 200
|        |      |Commands|                                                   |
|        |----> | * SLPF |-------------------------------+                   v               ^
|        |      | * ...  |                               |                                   |
|        |      +--------+         +-------------+       |----------> "action":"deny"        |
|        |                         |Serialization|       |            "target":"ipv4_addr"   |
|        |-----------------------> | * JSON      |-------+                                   |
|        |                         | * CBOR      |                           |               |
+--------+                         +-------------+                           |               |
                                                                             v               |
                                                                          +-- ------------------+
                                                                          |      Consumer(s)    |
                                                                          +---------------------+

```

# Producers and Consumers

OK, so what are OpenC2 _Producers_ and _Consumers_?

* **Producers** send Commands to Consumers. If you want to defend
  your network, your network nodes will be OpenC2 Consumers,
  awaiting commands from your Producer(s). The Producer could be
  a command-line script that you run manually, one of your
  Consumers, or a billion dollar orchestration system. It doesn't
  matter.
* **Consumers** act when given a Command, and reply to Producers
  with Responses.



# Message: Request or Response

An OpenC2 Message is a Request (AKA Command) OR Response.

* **Requests** are sent by Producers to Consumers. There can only
  be ONE Request in a Message.
* **Responses** are sent by Consumers to Producers. There can
  only be ONE Response in a Message

Again, notice how we didn't mention anything about Transfer,
Serialization, or even what the commands are yet? We also haven't
said how many Responses are generated for any Commands, or
when/how they're sent. Will we? Perhaps...

**Request Payload**
```
Fields:                  Description:                                       JSON Example:                        
                                           
action     : Required    Do this ...                                       "action"     : "deny"                 
target     : Required            ... To this                                "target"     : {"ipv4_net ...         
actuator   : -           Use this if you have it, otherwise do nothing     "actuator"   : {"slpf": ...           
args       : -           When to do it, if to reply..                      "args"       : {"response_req...      
command_id : -           Bookkeeping                                       "command_id" : "12345"                
```

**Response Payload**
```
Fields:                    Description:                            JSON Example:

status      : Required     Machine readable result of a Command    "status"      : 200
status_text : -            Human readable result                   "status_text" : "The command succeeded"
results     : -            Data you asked for in the Command       "results"     : {"slpf" : {"rule_num...
```

# Message: Headers

The forgotten children of OpenC2: The Headers. They're called
[Common Message
Elements](https://docs.oasis-open.org/openc2/oc2ls/v1.0/cs02/oc2ls-v1.0-cs02.html#32-message)
in the Language Spec, but their implementation details are in the
Transfer specs, because 'headers' is very dependent on transport
protocol. They tell you if the payload is a Request or Response,
in JSON or something else, etc.

**These are not _fields_ to populate, unlike "action" and
"target", etc.** These are *names of data*, and that data may go
into the header fields of an OpenC2 message, the fields of your
transfer headers, or both.

**Message Headers (but not actual Headers...)**
```
content_type : Is the payload JSON?
msg_type     : Is the payload an OpenC2 Command or Response?
request_id   : Easily conflated with "command_id", but can be used to help group commands. Again, look in your Transfer Spec.
...          : Many more that are dependent on the Transfer Spec.
```

Notice that some *look* very similar to HTTP headers.

For example, here's how the DATA of **"content_type"** and
**"msg_type"** is put into the HTTP Header **"Content-type"**.
Note the casing and dash. We also stuck in the version for good
measure.

```
HTTP Header:
                     This message is an
                     OpenC2 message!
                            |            Using this
                            |            OpenC2 Version
                            |             |
                            v             v           

Content-type: application/openc2+json;version=1.0
                    
                                   ^
                                   |
                                   |
                                Serialized with JSON!
```
    
How did we know how to format it? You would only know by reading
the [HTTPS Transfer
Spec](https://docs.oasis-open.org/openc2/open-impl-https/v1.0/open-impl-https-v1.0.html).

# Command: Action/Target Pair

In an OpenC2 **Request** Message, the only required payload is an
**action** and **target** pair. This pair constitutes a
**Command**. This is the bread-and-butter of OpenC2, the biggest
selling point, and what makes it so simple and powerful. Is there
a bad-guy coming in on some IP Address? Block him with 

```
"action" : "deny",
"target" : {"ipv4_net" : ["...."]}
```
The basic JSON syntax is shown below. 

One reason the syntax and format of commands doesn't feel too
well-defined in the specs is, again, they're not defined directly
in a Serialization format like JSON, but instead are defined
abstractly, and it's inferred that those abstract definitions can
map to *any* concrete serialization. But this isn't stated out
loud, leaving some obvious tension between "We're not dipping our
toes in serialization directly" and "Well, we recognize you need
some hints on how to actually implement this." That's why there
are a lot of examples in JSON, but with asterisks saying "This
section is non-normative".

For the simplicity and to actually implement something, for this
discussion let's assume OpenC2 messages are always JSON.


Back to the Action/Target pair:

```
     Action is always a single-word, eg "deny"
           |
           v
           
"action":  "deny"
"target":  {"ipv4_net" : ["192.168.17.0/24"]}

           ^             ^
           |             |
           |             Type and value here depend on the target.
     Target is           For ipv4_net in json, it's a one-value array.
     always a one-key          
     dictionary, e.g., 
     {"ipv4_net": ...}
     
 - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 

                              We could also have another dictionary, 
                              as with target ipv4_connection:
                               |
                               v 
"action": "deny" 
"target": {"ipv4_connection" : {"protocol": "tcp",
                                "src_addr": "1.2.3.4"} }
```

**The "action" field is obviously simple**; it's just one word,
and can *only* be a word from the actions listed in the Language
Spec. Those actions are the "verbs" of OpenC2.

**"target" is its own beast.** Sure, it's always a
one-key-dictionary, with the key a word from the Language Spec
targets (usually -- there are provisions for extensions), but
what about the value of that dictionary? For example, 

How did we know that ipv4_net is a one-value string array?

    ["192.168.17.0/24"]

It's actually complicated to figure out, and this is one of the
barriers-to-entry we mentioned earlier. Instead of prescribing
exactly how to format something in JSON, we have to deduce the
format for ANY serialization.

Here's one way to figure out **ipv4_net** in **JSON**. Read at
your own peril.

1. Search for examples in any of the OpenC2 specs that use
   **ipv4_net**.
2. Can't find any? Look in the language spec for its **type**.
3. That type is **IPv4-Net**. Notice the capitalization and dash.
4. Search the Language Spec for that.
5. We find 6 references. Look for one that begins with **Type:
   IPv4-Net (Array /ipv4-net)**
6. In the table there we see 2 values: **IPv4-Addr** and
   **Integer**
7. ~~Search the Language Spec for each of those.~~
8. Just kidding. Your next move is to read the text *above* that
   table.
9. The fourth line there says, **"JSON serialization of an IPv4
   address range SHALL use the 'dotted/slash'.."**
10. Ok, now we know to use "192.168..../24" style addresses, but
    how do we know to put it into a JSON array? A one-value
    array???
11. Go back to the *first* line, which reads "An IPv4 address
    range... **consists of two values**, an IPv4 address and a
    prefix."
12. From there, we can guess that we are dealing with an array
    because of **"..two values.."**, and the fact that we saw the
    word "Array" in **Type: IPv4-Net (Array /ipv4-net)**
13. What is **(Array /ipv4-net)**? It does look like a type
    definition, but I don't recognize the language.

So now, we are **PRETTY SURE** that a JSON formatted `ipv4_net` value is

    ["192.168.17.0/24"]

Congratulations!

# Actuators

Before we look at the **actuator field** of an OpenC2 Command, we
need to know what an actuator is.

**An actuator is a Consumer's implementation of an Actuator
Profile.**

# Actuator Profiles

An **Actuator Profile** (AP for short) is a document that defines
your commands and what they do. For example, the **[Stateless
Packet Filter Actuator Profile
(SLPF)](https://docs.oasis-open.org/openc2/oc2slpf/v1.0/oc2slpf-v1.0.html)**
grabs a bunch of actions and targets from the Language Spec,
pairs them up as individual commands, then declares what those
commands should do. On top of that, it gives itself a standard
name: **"slpf"** (known as a namespace identifier "nsid").

```
+---------------------+                   +-------------------------+
|  OpenC2 Language    |                   | Stateless Packet Filter |
|                     |                   | Actuator Profile        |
|  Actions:  +----------------+           |                         |
|   deny              |       |           | nsid:                   |
|   allow             |       |           |  "slpf"                 |
|   start             |       |           |                         |
|   stop              |       +---------> | pairs:                  |
|   ...               |       |           |  deny  ipv4_net         |
|                     |       |           |  deny  ipv4_connection  |
|  Targets: +-----------------+           |  allow ipv4_net         |
|   ipv4_net          |                   |  allow ipv4_connection  |
|   ipv4_connection   |                   |  ...                    |
|   mac_addr          |                   |                         |
|   ...               |                   |                         |
+---------------------+                   +-------------------------+


```

**Consumers implement Actuator Profile(s)**

So, if we have a Consumer that implements the SLPF Actuator
Profile, the Consumer **has** an SLPF Actuator.

It's not complicated, but one analogy that helps is the
following:

![laptop_stickers](/images/laptop_sticker.png)

In this analogy, the laptop is a Consumer, and the stickers
advertise the Actuator Profiles it implements. 
* The **Windows sticker** advertises a user interface you are
  familiar with that has a **"start" command**. 
* If there was a **Blu-ray Disc sticker**, you would expect to
  find a disc drive with an **"open/close" command**.

In the OpenC2 world, **if we saw an "slpf" sticker, we would
expect support for the "deny ipv4_net" command.**

Well, where are the stickers in OpenC2? There are three kinds:

* **Discovered**: You send the Consumer a command called
  **`query-features`**, and it tells you the Actuator Profiles it
  implements. That's the only command that *all* Consumers must
  implement, and the only one that isn't specific to any
  particular Actuator.
* **Pre-Shared**: You **configured** the Consumer, so you already
  know the Actuator Profiles it implements.
* **Unknown**: You don't know what the Consumer implements,
  but you just send it commands because this is an emergency and
  we don't have time to play games.

Ok, back to using the **actuator field** in an OpenC2 Command.

# Command: Actuator Field
### This field helps a Consumer determine if it should act on a command.

Remember, the only required fields in an OpenC2 Command are the
**`action`** and **`target`**.

`"actuator" : {}` --> *Actuator field is blank or omitted. Anyone
with this action/target pair, please act.*

Well, what if we need to filter out some Consumers, even if they
have the action/target pair we sent? Sure, you could just not
send them a command to begin with, but that isn't always
feasible.

Two fundemental filter scenarios:

1. **Filtering out Shotgun Commands**: Producers may **SPAM**
   Consumers with commands that don't apply to those Consumers,
   and the Consumers need a way to know which commands are
   applicable to them. 
    * `"actuator" : {"slpf": {"named_group": "perimeter82"}}` -->
      *Not only must the action-target pair match, but only
      Consumers with SLPF that are a member of the perimeter82
      group should act on this command*
    * `"actuator" : {"slpf": {} }` --> *Not only must the
      action-target pair match, but the Consumer must have and
      use its SLPF actuator*
1. **Multiple Actuator Profiles**: Consumers may implement more
   than one Actuator Profile, with duplicate action/target pairs.
    * `"actuator" : {"slpf": {} }` --> *I need the SLPF actuator
      to execute this action-target pair, even though this poorly
      designed Consumer has other Actuators with the same
      action-target*


## Example

Say we have the following Actuator Profiles:


| Actuator Profile | Description |
|-|-|
|slpf | Stateless Packet Filter, supports **`deny ipv4_net`** |
|x-trouble | Unknown, but supports **`deny ipv4_net`**  |
|x-acme | RoadRunner Hunting |

And Consumers that implement them:

|Consumer |Actuator Profile(s)|  Duplicate Action-Target Pairs (besides query-features) |
|:-:|-|-|
|1|slpf |  -|
|2|x-trouble |  - |
|3|x-acme |  - |
|4|slpf + x-acme | **none** |
|5|slpf + x-trouble | **deny ipv4_net** |

We send these consumers the same command:

```
"action" : "deny",
"target" : {"ipv4_net": ["192.168.1.0/24"]}
```

And sometimes we include the actuator field specifying SLPF:

```
"actuator" : {"slpf" : {}}
```

What does the Consumer do, assuming it processed the command
successfully if able? How does it respond?


| Consumer | Actuator Profiles  |"actuator": {} | "actuator": {"slpf": {}} |
|-|-|:-|:-|
|1|slpf| &#x2705; 200 OK             | &#x2705; 200 OK |
|2|x-trouble|&#x2705; 200 OK             |:negative_squared_cross_mark: 404; not found |
|3|x-acme| :negative_squared_cross_mark: 404; not found   |:negative_squared_cross_mark: 404; not found |
|4|slpf + x-acme| &#x2705; 200 OK                                                          |&#x2705; 200 OK |
|5|slpf + x-trouble| &#x274C; Behavior **and** Response are UNDEFINED  |&#x2705; 200 OK |


The most obvious lesson here is that you should avoid defining
Consumers that contain duplicate action-target pairs.

# Command ID vs Request ID

When you start asking 

> "I received a response message; what command triggered this?" 

you've run into the need for correlation. One of the items
included in the "names of data" discussed above in the [Message:
Headers](#message-headers) section is the OpenC2 `request_id`,
defined as 

>"A unique identifier created by the Producer and copied by
>Consumer into all Responses, in order to support reference to a
>particular Command, transaction, or event chain." 

So, where does the Producer put the `request_id`? Where does the
Consumer copy it to? There are two answers, and both of them can
be "right".

**Answer #1:  put it in the OpenC2 message headers**<br>(wait,
before we said those weren't really headers)

As of version 1.1 of the [Language
Specification](https://github.com/oasis-tcs/openc2-oc2ls/blob/working/oc2ls.md),
OpenC2 is adopting an "atomic" [message
structure](https://github.com/oasis-tcs/openc2-oc2ls/blob/working/oc2ls.md#32-message)
with actual headers. One of those is `request_id`, so you can put
your unique identifier in that field in your Request message and
it will be returned in the corresponding field in the Response
message. Voila, correlation!

**Answer #2:  use the features of your transfer protocol**

Many transfer protocols also offer support for correlation, such
as the (non-standard but common) HTTP `X-Request-ID /
X-Correlation-ID` field. So you can also achieve request /
response correlation using protocol features. 

**Both Right: put them in both places!**

Sometimes the right answer is to put that unique identifier in
both places, so that your OpenC2 Producers and Consumers can help
with correlation, but you can also take advantage of protocol
features.

When in doubt, look to the OpenC2 transfer specification for the
transfer protocol you've selected for your application and follow
its guidance. If you're breaking fresh ground with a new transfer
protocol, consider the existing transfer protocol specs useful
examples.



# Query Features

What commands can your Producer send to your Consumer? There is
always one command that is required to be implemented on your
Consumers:

```
{
    "action": "query",
    "target": {
        "features": ["versions", "profiles", "rate_limit"]
    }
}
```
     
This is probably the first command your Producer will send out.
The Response will tell you everything you need to know about the
Consumer that received the Command, including what other commands
it implements.


# Acknowledgement

The editors would like to recognize [Mr. Patrick Connole](https://github.com/patconnole) as the author of the [original version](https://github.com/patconnole/openc2_companion) of this very helpful document.