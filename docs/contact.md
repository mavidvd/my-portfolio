# Get in touch!

Let's Talk about Data! Always glad to hear from you.

# Contact Me

<form id="contact-form" action="https://formspree.io/f/mnngkdjo" method="POST">
  <input type="hidden" name="_subject" id="email-subject">
  
  <label>
    Your name:
    <input type="text" name="name" id="name-input" required>
  </label>
  
  <label>
    Your email:
    <input type="email" name="email" id="email-input" required>
  </label>
  
  <label>
    Subject:
    <input type="text" name="subject" id="subject-input" required>
  </label>
  
  <label>
    Your message:
    <textarea name="message" id="message-input" required></textarea>
  </label>
  
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
  margin: 2rem 0;
}
label {
  display: block;
  margin: 1rem 0;
  font-weight: bold;
}
input, textarea {
  width: 100%;
  padding: 0.5rem;
  margin-top: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  background: #1e1e1e;
  color: #fff;
}
textarea {
  min-height: 150px;
}
button {
  background: #1976d2;
  color: white;
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}
button:hover {
  background: #1565c0;
}
</style>