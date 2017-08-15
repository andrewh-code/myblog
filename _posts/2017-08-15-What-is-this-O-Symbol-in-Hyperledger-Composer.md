---
layout: post
title: What is this 'O' Symbol in Hyperledger Composer?
---

During my blockchain exploration, I decided to put off learning Hyperledger Fabric due to the transition from v0.6 to v1.0 in the middle of this year. I read reports, summaries, and articles that v1.0 would be vastly different from v0.6 and I realized that if I learned v0.6 now, then I would have to learn it all over again for v1.0, similar to AngularJS vs. Angular2 or is it Angular4 now? 

That would be a waste of time. Now the time has come to start learning Hyperledger because they have finally released v1.0 and now I’m cracking into Fabric and Fabric Composer. I don’t think I will get into the other types of blockchain technologies under the Hyperledger project (Iroh, Sawtooth, etc).

I started learning Hyplerledger Composer recently after doing stuff on Fabric and the one thing that threw me off was how they created the model/data files. It’s very similar to how you create a model class/object in another language that supports OOP (whether it be Java, GoLang, PHP, or Python), you pretty much do the same with Hyperledger Fabric and Composer.
Here’s an example of a data model file in Hyperledger Composer. The file (.cto, I still don’t know what .cto stands for) is used to define the business network.

```
/** * Defines a data model for a blind vehicle auction */

namespace org.acme.vehicle.auction 

asset Vehicle identified by vin {  
    o String vin  
    --> Member owner
} 
enum ListingState {  
    o FOR_SALE  
    o RESERVE_NOT_MET  
    o SOLD
}

asset VehicleListing identified by listingId {  
    o String listingId  
    o Double reservePrice  
    o String description  
    o ListingState state  
    o Offer[] offers optional  
    --> Vehicle vehicle
} 

abstract participant User identified by email {  
    o String email  
    o String firstName  
    o String lastName
} 

participant Member extends User {  
    o Double balance
} 

participant Auctioneer extends User {} 

transaction Offer {  
    o Double bidPrice  
    --> VehicleListing listing  
    --> Member member
} 
transaction CloseBidding {  
    --> VehicleListing listing
}
```


As you can see there are familiar OOP concepts in use in this [model file](https://github.com/hyperledger/composer-sample-networks/blob/master/packages/carauction-network/models/auction.cto "Hyperledger Composer Car Auction Network Example"). If you are familiar with OOP, then it shouldn’t be too hard to understand this model file. What really threw me off when I first saw this:

```
asset Vehicle identified by vin {  
    o String vin  
    --> Member owner
}
```

When you look at this `asset` definition for the `Vehicle` you notice its attributes. You can tell from how it’s designed that the `vin` is a String variable and the `owner` is a referenced variable/object of type Member which is a custom participant data type. I recognized the `-->` notation from my C programming days but this `o` symbol…what is this special symbol?


OK, this symbol probably helps differentiate between referenced variables/data types and the ones that the object/asset directly has. Why would they use a symbol like this? What the hell? It looks like a bullet point that you see in Microsoft Word. What’s the ASCII code for this bullet point? Why would they use such sort of thing, wow, this is stupid. All those ideas and questions were filling my head and for the life of me, I couldn’t figure out how to get this symbol. I guess I had to copy and paste the example composer projects in mine and keep copy/pasting when I created my own.
Then I read through the [modelling language documentation](https://hyperledger.github.io/composer/reference/cto_language.html) used in Hyperledger Composer. I finally got to this one specific subsection:


```
5. A set of named properties. The properties must be named, and the primitive data type defined.The properties and their data are owned by each resource, for example, a Car asset has a vin, and a model property, both of which are strings.
```

WHAT?!?!?! OMG this symbol is an ‘o’? As in type the letter ‘o’ on my keyboard ‘o’? ooooohhhhhhhhh! So I tried it in my .cto file and would you look at that, it is actually an ‘o’. Now I know why they used it, cause it’s an owned property. So that totally messed me up, I really did not expect that they would use an every day letter to represent a specific type of variable.


    - Andrew