##Family talk

This recipe will make your Angular components talk. Asynchronously.

Source: [Angular docs](https://angular.io/docs/ts/latest/cookbook/component-communication.html#!#bidirectional-service)

###Ingredients
- A parent component. If there isn't one, create it.
- Child component(s) which need to communicate
- A service
- A `subject`, available in your nearby RxJS module.

###Step 1: The service
Create a service. Angular CLI will create one for you automatically, but you still need to `provide` it. 
Include it in the providers array **only** in the Parent.
Import it in your parent and child components and inject it using their constructors.

###Step 2: The subject

A subject can be though of as both an Observable and an observer.
Create a subject of the thing you need, like this:

```javascript
export class FamilyService {
  // Observable string sources
  private thingYouWillNeed = new Subject<number>();
  
  // Observable string streams
  thingYouWillNeed$ = this.thingYouWillNeed.asObservable();
  
  // Service message commands
  whenSomethingHappens(communicateThis: number) {
    this.thingYouWillNeed.next();
  }
}

```


###Step 3: The trigger
Say there are two children, and ElderBro wants to communicate with YoungerBro. 
It needs to bind the right event to a method which uses our service's `whenSomethingHappens()`

```javascript
...
export class ElderBro {

  //service injected here, it's the same instance as the one with parent
  constructor(private familyService: FamilyService) { } 

  sendMoney(cashAmount){ // could be called from somewhere in the HTML Template
      this.familyService.whenSomethingHappens(cashAmount)
  }

}
```

###Step 4: The subscription

The listening component then reacts to the event. It does so by subscribing the the observable from the service

```javascript
...
export class YoungerBro {

  //service injected here, it's the same instance as the one with parent
  //subscription is defined here
  constructor(private familyService: FamilyService) {
      familyService.thingYouWillNeed$.subscribe(cash => {
          this.useCash(cash)
      })
  } 

  useCash(cashAmount){ // called whenever the subscription fires
      buyBeer()
      eatOut()
      buyJewelleryForGf()
  }

}

You now have a family which can communicate properly.



