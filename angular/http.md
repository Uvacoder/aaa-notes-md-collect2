# http

- All `HttpClient` methods return an RxJS Observable of something.

- HTTP is a request/response protocol. You make a request, it returns a single response.

- In general, an observable can return multiple values over time. An observable from HttpClient always emits a single value and then completes, never to emit again

## Example

```javascript
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Hero } from './hero';

/** GET heroes from the server */
@Injectable({
  providedIn: 'root'
})
export class HeroService {
  private heroesUrl = 'api/heroes';  // URL to web api

  getHeroes (): Observable<Hero[]> {
    return this.http.get<Hero[]>(this.heroesUrl)
  }
  constructor(private http : HttpClient){

  }
}
```

This particular `HttpClient.get` call returns an `Observable<Hero[]>`, literally "an observable of hero arrays". In practice, it will only return a single hero array.

## HttpClient.get

`HttpClient.get` returns response data  
`HttpClient.get` returns the body of the response as an untyped JSON object by default. Applying the optional type specifier, <Hero[]> , gives you a typed result object.

## HTTP Error handling

To catch errors, you `pipe` the observable result from `http.get()` through an RxJS `catchError()` operator.

import

```javascript
import { catchError, map, tap } from 'rxjs/operators';
```

codechange

```javascript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl)
    .pipe(
      catchError(this.handleError<Hero[]>('getHeroes', []))
    );
}
```

The `catchError()` operator intercepts an `Observable` that failed. It passes the error an error handler that can do what it wants with the error.

In the above code they are passing a error handler called `handleError` which must be defined

## http.put

The `HttpClient.put()` method takes three parameters

1.the URL
2.the data to update (the modified hero in this case)
3.options

