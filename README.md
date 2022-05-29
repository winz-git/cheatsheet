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
