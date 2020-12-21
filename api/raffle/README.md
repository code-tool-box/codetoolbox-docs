# Raffle Endpoint

**Usage**
---
  <_This endpoint will pick a X quantity of random numbers between a max and min values._>

* **URL**

  `/0.1/raffles`


* **Method Allowed:**
  
  `POST`

* **OAuth**	

  _Not Required_
  
* **URL Params**

   _None_

* **Data Params**

  <_This endpoint recieves a JSON with three params as follow:_>

  Param | Type | Comments
  ------------ | ------------- | -------------
  n1 | number | Initial number that will be used for randomize the results
  n2 | number | Final number that will be used for randomize the results
  nr | number | How many numbers will be randomized between initial and final number

  <_This JSON Object will looks like:_>

  ```json
  {
    "n1": 1,
    "n2": 100,
    "nr": 1
  }
  ```

* **Success Response:**
  
  <_The result will be an array with the number or numbers required by the user between the min and max numbers given._>

  * **Code:** 200 OK <br />
    **Content:** `[48]` <br />
    **Message:** `{ "message": "Raffle numbers on the way!" }` <br />
    **Entire Response** <br />
    ```json
    {
    "result": [
        48
    ],
    "response": {
        "success": true,
        "message": "Raffle numbers on the way!",
        "status": 200
    },
    "validations": null
    }
    ```

* **Error Response:**

  <_This endpoint has some validations and error treatments as follow:_>

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `null` <br />
    **Message:** `{ "message": "Final number is required!" }` <br />
    **Validation Message:** `{ "validations": "Field n2 cannot be null." }` <br />
    **Entire Response** 
    ```json 
    {
      "result": null,
      "response": {
        "success": false,
        "message": "Final number is required!",
        "status": 422
      },
      "validations": "Field n2 cannot be null."
    }
    ```

  * **Code:** 503 SERVICE UNAVAILABLE <br />
    **Content:** `{ "error": "Service Unavailable!" }`

* **Sample Call:**

  <_Typescript example:_>

  ```typescript
  public getRaffle(n1, n2, nr) {
    const data = {
      n1,
      n2,
      nr
    }
    this.http.post('https://codetoolbox.com.br/api/0.1/raffles', data).toPromise().then((res) => {
      console.log(res);
    });
  } 
  ```



* **Methods NOT Allowed:**
  
  `GET` | `DELETE` | `PUT`

* **Methods NOT Allowed Response:**

  * **Code:** 418 I'M A TEAPOT <br />
    **Content:** `null` <br />
    **Message:** `{ "message": "Not Implemented Yet!" }` <br />
    **Entire Response**
    ```json 
    {
      "result": null,
      "response": {
          "success": false,
          "message": "Not Implemented Yet!",
          "status": 418
      },
      "validations": null
    }
    ```