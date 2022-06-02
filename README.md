# cheatsheet

## Typescript

### Retry fetch

```javascript
interface retryPromiseOptions<T>  {
    retryIf?:(response:T) => boolean, 
    retries?:number
}

function retryPromise<T>(promise:() => Promise<T>, options:retryPromiseOptions<T>) {
    const { retryIf = (_:T) => false, retries = 1} = options
    let _promise = promise();

    for (var i = 0; i < retries; i++)
        _promise = _promise.then((value) => retryIf(value) ? promise() : Promise.reject(value));
    
    return _promise;
}


Usage:
-----------------------------------

retryPromise(fetch(url),{
    retryIf: (response:Response) => true, // you could check before trying again
    retries: 5
}).then( ... my favorite things ... )


-----------------------------------


```

## Javascript
### Spread Operator

Update a property of all items
```
rows.map((item) => ({...item, role: 'user'})
```

Set an item to be on top of array
```
[rows.filter( x => x.id === id)[0], ...rows.filter( x => x.id !== id )]
```
