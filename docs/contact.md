# Book a call or connect with me.

<div style="text-align: center; 
            margin-top: 1.5em; 
            margin-bottom: 1.5em;
            margin-right: 6em;
            /* CRUCIAL STYLES BELOW */
            display: flex; 
            justify-content: center;
            flex-wrap: wrap; /* Allows tags to wrap if screen is small */
            gap: 15px; /* Sets space between items */
            ">

    <link href="https://assets.calendly.com/assets/external/widget.css" rel="stylesheet">
    <script src="https://assets.calendly.com/assets/external/widget.js" type="text/javascript" async></script>

    <a href="" 
       onclick="Calendly.initPopupWidget({url: 'https://calendly.com/davidmagraner/30min'});return false;" 
       class="tag">
        <span>Book a 30' Call</span>
    </a>
    
    <a href="https://www.linkedin.com/in/davidmagraner/" 
       target="_blank" 
       class="tag">
        <i class="fab fa-linkedin"></i> Connect on LinkedIn
    </a>
    
    <a href="https://github.com/mavidvd" 
       target="_blank" 
       class="tag">
        <i class="fab fa-github"></i> View My GitHub
    </a>

</div>

# Get in touch!
<form id="contact-form" action="https://formspree.io/f/mnngkdjo" method="POST">
  <input type="hidden" name="_subject" id="email-subject">
  
  <div class="form-row">
    <label for="name-input">Your name:</label>
    <input type="text" name="name" id="name-input" required placeholder="Enter your name">
  </div>
  
  <div class="form-row">
    <label for="email-input">Your email:</label>
    <input type="email" name="email" id="email-input" required placeholder="name@example.com">
  </div>
  
  <div class="form-row">
    <label for="subject-input">Subject:</label>
    <input type="text" name="subject" id="subject-input" required placeholder="What are you interested in?">
  </div>
  
  <div class="form-row">
    <label for="message-input">Your message:</label>
    <textarea name="message" id="message-input" required placeholder="Tell me about your project..."></textarea>
  </div>
  
  <button type="submit">Send</button>
</form>

<div id="form-status"></div>

<script>
document.getElementById('contact-form').addEventListener('submit', async function(e) {
  // 1. Prevent the default form submission (the one that redirects)
  e.preventDefault();
  
  const form = e.target;
  const statusDiv = document.getElementById('form-status');
  const button = form.querySelector('button');
  
  // Disable button and show loading
  button.disabled = true;
  button.textContent = 'Sending...';
  statusDiv.innerHTML = ''; // Clear previous status
  
  // 2. Prepare form data using the form element itself (more reliable)
  const formData = new FormData(form);
  
  // 3. Set the hidden _subject field content before sending
  // The correct subject format should be handled by the client-side
  const subjectValue = document.getElementById('subject-input').value;
  formData.set('_subject', '[From Portfolio] ' + subjectValue);

  // 4. Formspree recommends the 'Accept' header for JSON response
  try {
    const response = await fetch(form.action, { // Use form.action for the URL
      method: 'POST',
      body: formData,
      headers: {
        'Accept': 'application/json'
      }
    });
    
    // 5. Check if the response was successful
    if (response.ok) {
      statusDiv.innerHTML = '<p style="color: #4caf50; margin-top: 1rem; font-size: 1.2rem; font-weight: bold;">✓ The message has been correctly delivered. Thank you!</p>';
      form.reset(); // Clear the form fields
    } else {
      // Handle server-side validation or other errors
      const data = await response.json();
      let errorMessage = '✗ Oops! There was a problem sending your message. Please try again.';
      if (data.errors) {
        // Display specific error if Formspree provides one
        errorMessage += ' Details: ' + data.errors.map(err => err.message).join(', ');
      }
      statusDiv.innerHTML = '<p style="color: #f44336; margin-top: 1rem;">' + errorMessage + '</p>';
    }
  } catch (error) {
    // Handle network errors (e.g., no internet connection)
    statusDiv.innerHTML = '<p style="color: #f44336; margin-top: 1rem;">✗ Network error. Please check your connection and try again.</p>';
  }
  
  // Re-enable button
  button.disabled = false;
  button.textContent = 'Send';
});
</script>

<style>
/* Existing styles remain the same */
form {
  max-width: 600px;
  
  /* 👇 CHANGE 1: Remove text-align: center (no longer needed here) */
  /* text-align: center; */
  
  /* 👇 ADD THIS RULE to center the entire form block on the page */
  margin-left: auto;
  margin-right: 8rem;
}

/* New rule for the container div */
.form-row {
  display: flex;
  align-items: flex-start;
  margin-bottom: 25px;
}

/* Style the label (the text on the left) */
.form-row label {
  color: #E0A465;  
  font-weight: bold;
  min-width: 150px; 
  padding-top: 10px;
}

/* Style the inputs (the boxes on the right) */
input, textarea {
  flex-grow: 1; 
  padding: 0.7rem;
  margin-top: 0;
  border: 1px solid #ccc;
  border-radius: 15px;
  background: #1e1e1e;
  color: #fff;
  transition: border-color 0.3s;
}

textarea {
  min-height: 80px;
}

input:focus, textarea:focus {
  outline: none;
  border-color: #1976d2;
}

label {
  display: inline-block;
}

button {
  /* 👇 CHANGE 2: Center the button's text/content (optional, but good practice) */
  display: block; 
  margin: 15px auto 0 auto; /* Sets top margin to 15px, and auto left/right margin for centering */
  
  background: #142F5A;
  color: white;
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
}
button:hover {
  background: #09386dff;
}
</style>