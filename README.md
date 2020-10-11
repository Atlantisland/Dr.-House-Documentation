**Dr. House Hospital**
=======
* **Overview**
-----------
  Dr. House hospital is a set of 4 web applications that communicate with each other in order to enable its management.

  1. Admission: the patient receives a unique identifier and goes to the Diagnoses. Only a REST client with the right credentials can access to use it.
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
    "symptoms": "headache"
    }
  ```
* **Result**

  ```javascript
    {
    "uuid": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69", 
    "name": "Lisa", 
    "symptoms": "headache"
    }
  ```
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
  
* **Result**

  ```javascript
    {
    "Lisa": "3bc716e1-9c68-4c42-bc89-62b4e9c67f69"
    }
  ```
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
  
* **Result**

  ```javascript
    {
    
    }
  ```
  

