## How I learned to stop worrying and ~~love~~ like Angular2. As a friend.

I remember the first time I got the chance to see a swiss army knife. It had about seventeen attachments, and I knew all of them did _something_, but I had no damn clue what. Then I saw the penknife and I was like, "AHA. I know THAT one. That's for cutting stuff." It would be a long time before I gained a healthy appreciation of all those scary tools.

Angular is like that. It has a lot of cool-but-scary-looking tools, and as I beginner I was only able to identify a few of them. The others look vaguely familiar, and yet hopelessly obtuse. But now I _think_ I've learned enough to appreciate what they've done and why.

I'm here to share that appreciation. Alright. Enough prologue. Let's go.

The prerequiste here is the Angular Quickstart guide and all the prerequisites you need to get to that.

The main files to concern ourselves with would be `app.module.ts` and `app.component.ts`. Speaking of `ts`, that's the extension for typeScript, Microsoft's roided-out version of JavaScript. Some IDEs still don't support it. I recommend Atom or VS Code.

TypeScript started out as a decent idea, but ES6 has severely bridged the gap between JS and TS. The major advantages TS now has are typecheking and interfaces. But the most compelling reason to use it is that in modern IDEs, if you use TS and screw up somewhere, you'll get a highlight and a warning _right in your editor_ without needing to compile or run anything.

Okay, back to the `AppModule`. This is what it looks like:

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

The interesting part is the stuff inside `@NgModule`. Basically, the bootstrap line is telling Angular that `AppComponent` is the root of out app. Angular will gift-wrap it and present it to `index.html`. Happy birthday. That's how the party starts.


There's a lot of other stuff to discuss here, including the scary looking`@`, but let's circle back to that. For now, suffice it to say that `AppModule` is like the sign-in sheet every component, service and pipe must register to before they can join the party.

