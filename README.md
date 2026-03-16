# CS472 - Homework 06

### Exercise 01: Blocking vs Non‑Blocking API

Create an Express application exposing two endpoints that perform a **CPU‑intensive calculation**.

Implement a function `function calculatePrimes(n)` that returns all prime numbers ≤ `n` as `{ "results": [2,3,5,7] }`

* Implement `GET /blocking/primes/:n` that intentionally blocks the event loop.
* Implement `GET /non-blocking/primes/:n` that uses child process not to block the event loopo.


### Exercise 02: Task Processing API

Create a **task processing API** that executes CPU‑intensive tasks using child processes.

Given the following Entity: `/tasks`, where each task:
``` json
{
 "id": number,
 "input": number,
 "status": "pending" | "processing" | "done",
 "result": number
}
```

Assuming tasks are stored either in memory, or using `node-localstorage`, each task calls `factorial(n)` and sends back the following response `{ "taskId": 1, "status": "pending" }`. The task status must be updated once the factorial calculation is finished in non-blocking way using child process.

Implement the following endpoints:

* Create Task `POST /tasks/:n`
* Get All Tasks `GET /tasks`
* Get Single Task`GET /tasks/:id`

#### Processing Logic
When a task is created:
1.  Create a child process
2.  Send the input `n`
3.  Child process calculates factorial
4.  Child process sends the result back
5.  Parent process updates task status to `"done"`

