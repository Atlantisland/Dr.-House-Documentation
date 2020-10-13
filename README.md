**Dr. House Hospital**
=======

  **Overview**
-----------
  Dr. House hospital is a set of 4 web applications that communicate with each other in order to enable its management.

  1. Admission: the patient receives a unique identifier (UUID) and goes to the Diagnoses. Only a REST client with the right credentials can access to use it.
  2. Diagnoses: the patient receives a diagnosis based on the symptoms and goes to the Treatments.
  3. Treatments: the patient receives the respective treatment that is saved in the database and goes to the Accountancy.
  4. Accountancy: the patient receives the respective invoice that is saved in the database. Only accountant with the right credentials can access to see the   invoices and mark them as paid.

  **1. Admission**
-----------
  Registers the patient with name and symptoms, provides a UUID and returns it.

* **URL**

  /patients

* **Method**

  `POST`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  `uuid=[string]`
  
  `name=[string]`
  
  `symptoms=[string]`
 
* **Request**

  ```javascript
    { 
    "name": "Lisa", 
    "symptoms": "fatigue, appear pale"
    }
  ```
* **Success Response**

  * **Code:** 200 <br />
    **Content:** 
    
    ```javascript
       {
        "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69", 
        "name": "Lisa", 
        "symptoms": "fatigue, appear pale"
       }
    ```
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{error : "You are unauthorized to make this request."}`

 Returns all the registered patients.
  
* **URL**

  /uuids

* **Method**

  `GET`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  None
  
* **Success Response**

  * **Code:** 200 <br />
    **Content:** 
    
    ```javascript
       {
       "Lisa": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69"
       }
    ```
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{error : "You are unauthorized to make this request."}`
  
 Returns the patient with the specific name if the patient had been admitted, otherwise returns null.
  
* **URL**

  /uuids/{patientName}

* **Method**

  `GET`

* **URL Params**

  **Required**

  `patientName=[string]`
  
* **Data Params**

  None
  
* **Success Response**

  * **Code:** 200 <br />
    **Content:** 
    
     ```javascript
        {
        "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
        "name": "Lisa"
        }
     ``` 
    
* **Error Response:**

  * **Code:** 404 NOT FOUND <br />
    **Content:** `{error : "Patient does not exist"}`
    
  OR

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{error : "You are unauthorized to make this request."}`
  
**2. Diagnoses**
-----------
  Diagnoses the patient, logs a message and returns it.

* **URL**

  /patients

* **Method**

  `POST`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  `uuid=[string]`
  
  `name=[string]`
  
  `symptoms=[string]`
 
  `diagnosis=[string]`
 
* **Request**

  ```javascript
    { 
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa", 
    "symptoms": "fatigue, appear pale"
    }
  ```
* **Response**

  ```javascript
    {
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa",
    "symptoms": "fatigue, appear pale",
    "diagnosis": "anemia"
    }
  ```
    
 **3. Treatments**
-----------
  Provides a Treatment for the Patient, saves it in the database, and returns it.

* **URL**

  /patients

* **Method**

  `POST`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  `uuid=[string]`
  
  `name=[string]`
  
  `symptoms=[string]`
 
  `diagnosis=[string]`
  
  `treatment=[string]`
 
* **Request**

  ```javascript
    { 
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa", 
    "symptoms": "fatigue, appear pale"
    }
  ```
* **Response**

  ```javascript
    {
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa",
    "symptoms": "fatigue, appear pale",
    "diagnosis": "anemia",
    "treatment": "spend one day in the hospital bed"
    }
  ```
  Returns a list of all the Treatment entries that are saved in the database.
  
* **URL**

  /treatments

* **Method**

  `GET`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  None
  
* **Response**

  ```javascript
    {
     [{
       "uuid" : "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
       "name" : "Lisa",
       "symptoms" : "fatigue, appear pale",
       "diagnosis" : "anemia",
       "treatment" : "spend one day in the hospital bed"
      }]
    }
  ```
  
  Returns a list of all the Treatment entries with the matching uuid that are saved in the database.
  
* **URL**

  /treatments/{uuid}

* **Method**

  `GET`

* **URL Params**

  **Required**

  `uuid=[string]`
  
* **Data Params**

  None
  
* **Response**

   ```javascript
    {
     [{
       "uuid" : "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
       "name" : "Lisa",
       "symptoms" : "fatigue, appear pale",
       "diagnosis" : "anemia",
       "treatment" : "spend one day in the hospital bed"
     }]
    }
  ```
**4. Accountancy**
-----------
  Finds the Patient by uuid or saves a new one if it did not exist. Then generates an Invoice for that Patient, saves the Invoice, and returns the PatientDTO.

* **URL**

  /patients

* **Method**

  `POST`

* **URL Params**

  **Required**

  None
  
* **Data Params**

  `uuid=[string]`
  
  `name=[string]`
  
  `symptoms=[string]`
 
  `diagnosis=[string]`
  
  `treatment=[string]`
 
* **Request**

  ```javascript
    { 
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa", 
    "symptoms": "fatigue, appear pale"
    }
  ```
* **Response**

  ```javascript
    {
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69",
    "name": "Lisa",
    "symptoms": "fatigue, appear pale",
    "diagnosis": "anemia",
    "treatment": "spend one day in the hospital bed"
    }
  ```
   Returns a list of all the Invoice entries that are saved in the database.
  
* **URL**

  /invoices

* **Method**

  `GET`

* **URL Params**

  **Required**

  None
  
* **Data Params**

   `cost=[double]`
  
  `paid=[boolean]`
  
  `patient=[Patient]`
  
* **Response**

  ```javascript
    {
    
    }
  ```
   Marks the Invoice with the matching id as paid in the database.
  
* **URL**

  /invoices/{id}/paid

* **Method**

  `PUT`

* **URL Params**

  **Required**

  `id=[long]`
  
  `paid=[boolean]`
  
* **Data Params**

  None
  
* **Response**

  ```javascript
    {
    
    }
  ```
