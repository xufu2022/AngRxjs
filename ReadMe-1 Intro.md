# Rxjs in Angular

-   Routing

    this.route.paramMap

    this.route.data

    this.router.events (donot know this)

-   Reactive Forms

    this.productForm.valueChanges

-   HttpClient

        getProducts(): Observable<Product[]> {
        return this.http.get<Product[]>(this.url);
        }

QA1:

    x = 5
    y = 3
    z = x + y    
    x = 7

Value is assigned when the expression is first evaluated, z does not react to changes in x or y

But what if we want to react to changes?

Options:

-   Getter Function

    get exPrice() {return price * quantity;}

-   Event Handler

    onQuantityChanged(newQty) {exPrice = price * newQty;}

-   RxJS

    //Declare an Observable

    qty$ = new Observable();

    //Emit when an action occurs

    onQuantityChanged(newQty) {qty$.emit(newQty);}

    // React to emissions

    exPrice$ = qty$.pipe( map(q => q * price) );

## Propagate Changes

Pseudo Code

    exPrice$ = qty$.pipe(
        map(q => q * price)
    );

    tax$ = exPrice$.pipe(
        map(p => p * 10.75%)
    );

    deliveryFee$ = exPrice$.pipe(
        map(p => p < 30 ? 5.99 : 0)
    );

## Composing Observables

    totalPrice$ = combine(
        exPrice$,
        deliveryFee$,
        tax$
    ).pipe(
        map([s,d,t] => s + d + t)
    );