<h1>Dr. House Hospital</h1>
<h2>Overview</h2>
<p>Dr. House hospital is a set of web applications that communicate with each other in order to enable its management.</p>
<p>Web applications:</p>
<ol>
<li>Admission: the patient receives a unique identifier and goes to the Diagnoses. Only a REST client with the right credentials can access to use it.</li>
<li>Diagnoses: the patient receives a diagnosis based on the symptoms and goes to the Treatments.</li>
<li>Treatments: the patient receives the respective treatment that is saved in the database and goes to the Accountancy.</li>
<li>Accountancy: the patient receives the respective invoice that is saved in the database. Only accountant with the right credentials can access to see the invoices and mark them as paid.</li>
</ol>
<h2>Admission</h2>
<p>Registers the patient with name and symptoms, provides a UUID and returns it</p>
<ul>
<li>URL</li>
</ul>



