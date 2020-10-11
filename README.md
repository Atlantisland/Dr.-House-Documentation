**Dr. House Hospital**
=======
* **Overview**
-----------
  Dr. House hospital is a set of 4 web applications that communicate with each other in order to enable its management.

  1. Admission: the patient receives a unique identifier and goes to the Diagnoses. Only a REST client with the right credentials can access to use it.
  2. Diagnoses: the patient receives a diagnosis based on the symptoms and goes to the Treatments.
  3. Treatments: the patient receives the respective treatment that is saved in the database and goes to the Accountancy.
  4. Accountancy: the patient receives the respective invoice that is saved in the database. Only accountant with the right credentials can access to see the   invoices and mark them as paid.

* **Admission**
-----------
  Registers the patient with name and symptoms, provides a UUID and returns it.

* **URL**

  /patients

* **Method**

  `POST`

* **URL Params**


