# Terms and Syntax

    RxJS
        subscribe() //Start
            - Emits items
        pipe() through a set of operators
        Observer
            - next()
            - error()
            - complete()
        unsubscribe() //Stop

## RxJS Features

of
from

## Observer

    Next item, process it next()
    Error occurred, handle it error()
    Complete, you're done complete()

## Observable

A collection of events or values emitted over time
- User actions
- Application events (routing, forms)
- Response from an HTTP request
- Internal structures

## Observable/Observer

Source with Observable, Observer can observes and reacts

## Observables Can Emit

- Primitives: numbers, strings, dates
- Events: mouse, key, valueChanges, routing
- Objects: customers, products
- Arrays
- HTTP response

## Observables

    const observer = {
        next: apple => console.log(`Apple emitted ${apple}`),
        error: err => console.log(`Error occurred: ${err}`),
        complete: () => console.log(`No more apples, go home`)
    };

    const apples$ = new Observable(appleSubscriber => {
        appleSubscriber.next('Apple 1');
        appleSubscriber.next('Apple 2');
        appleSubscriber.complete();
    });

## Subscribing

- Call subscribe() on the Observable

- Pass in the Observer

- MUST subscribe to start receiving emissions

Every time we subscribe to start, we should unsubscribe to stop

## Stop Receiving Notifications

- Call complete() on the subscriber
- Use an operator that automatically completes
- Throw an error
- Call unsubscribe() on the subscription

        sub.unsubscribe();

## of vs. from

    const apples = ['Apple 1', 'Apple 2'];

    of(apples);
    // [Apple1, Apple2]

    from(apples);
    // Apple1 Apple2

    of(...apples);
    // Apple1 Apple2

## Creating an Observable

@ViewChild('para') par: ElementRef;

ngAfterViewInit() {
    const parStream = fromEvent(this.par.nativeElement, 'click').subscribe(console.log)
}

const num = interval(1000).subscribe(console.log);
