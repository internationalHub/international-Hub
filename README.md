# International Hub Website

This site is built using HTML, CSS, JavaScript and PHP.

## Code Breakdown

/assets <br>
- /css - contains all the styling for the site <br>
- /img - contains images that are used throughout the site
- /js
    - main.js - contains JQuery code for the website animations
- /vendor - contains all external frameworks and technologies used within the code <br>

/forms <br>
- This is old code for the form that we are keeping for the time being. <br>

index.html - main page

## Form functionality

The form in the website works differently from the code in the forms folder.

The form on the site takes in information from the user (name, email and employment) and puts the information into a Google spreadsheet once the user clicks submit. 

Presently, there is a script (look below) at the bottom of the index.html file that handles the information that is put in by the user. 

```Javascript
const scriptURL = 'https://script.google.com/macros/s/AKfycbzZqBvFtuQTveQVI5r8jLfYx0vCFe9hh_MjVUTJeWGorLXhtmo/exec'
    const form = document.forms['submit-to-google-sheet']
    const loading = document.querySelector('.js-loading');
    const successMessage = document.querySelector('.js-success-message')
    const errorMessage = document.querySelector('.js-error-message')

    form.addEventListener('submit', e => {
      e.preventDefault()
      showLoadingIndicator()
      fetch(scriptURL, { method: 'POST', body: new FormData(form)})
        .then(response => showSuccessMessage(response))
        .catch(error => showErrorMessage(error))
    })

    function showLoadingIndicator () {
      form.classList.add('is-hidden')
      loading.classList.remove('is-hidden')
    }
    
    function showSuccessMessage (response) {
      console.log('Success!', response)
      setTimeout(() => {
        console.log("it went in");
        successMessage.classList.remove('is-hidden')
        loading.classList.add('is-hidden')
      }, 500)

      form.reset();
    }

    function showErrorMessage (error) {
      console.error('Error!', error.message)
      setTimeout(() => {
        errorMessage.classList.remove('is-hidden')
        loading.classList.add('is-hidden')
      }, 500)
    }
```

Each of the query selectors correspond to the code in the form tag. Below is the html code for the form:
```HTML
<form name="submit-to-google-sheet">
    <div class="subscribe-form">
        <input type="text" name="fullName" placeholder="Name" required>
        <input type="email" name="email" placeholder="Email" required>
        <select class="select-employment" id="employment" name="employmentType">
        <option value="default">Select employment type</option>
        <option value="student">Student</option>
        <option value="earlyprofessional">Early Career Professional</option>
        </select>
    </div>
    <button type="submit" value="Subscribe"> Subscribe</button>
</form>
```
For more information on how the information from the form is submitted to the spreadsheet, refer to this [documentation](https://github.com/jamiewilson/form-to-google-sheets). 

If you have any further questions, reach out to Deborah.