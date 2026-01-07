<script lang="ts">
  export let formTitle = "Send Us a Message";
  export let submitButtonText = "Send Message";
  export let showSubject = false;

  let name = "";
  let email = "";
  let phone = "";
  let subject = "";
  let message = "";
  let submitted = false;
  let submitting = false;

  async function handleSubmit() {
    submitting = true;
    // Simulate form submission
    await new Promise((resolve) => setTimeout(resolve, 1000));
    submitted = true;
    submitting = false;

    // Reset form
    name = "";
    email = "";
    phone = "";
    subject = "";
    message = "";
  }
</script>

<div class="max-w-xl mx-auto">
  <h3 class="font-serif text-2xl md:text-3xl text-gold mb-8 text-center">
    {formTitle}
  </h3>

  {#if submitted}
    <div class="text-center py-12 border border-gold/30 rounded-sm bg-dark/50">
      <i class="fa-solid fa-check-circle text-gold text-4xl mb-4"></i>
      <p class="font-serif text-xl text-white mb-2">Thank You!</p>
      <p class="text-gray-400">We'll be in touch soon.</p>
      <button
        on:click={() => (submitted = false)}
        class="mt-6 text-gold hover:text-white transition-colors text-sm uppercase tracking-wider"
      >
        Send Another Message
      </button>
    </div>
  {:else}
    <form on:submit|preventDefault={handleSubmit} class="space-y-6">
      <div>
        <label for="name" class="form-label">Name</label>
        <input
          type="text"
          id="name"
          bind:value={name}
          required
          class="form-input"
          placeholder="Your name"
        />
      </div>

      <div>
        <label for="email" class="form-label">Email</label>
        <input
          type="email"
          id="email"
          bind:value={email}
          required
          class="form-input"
          placeholder="your@email.com"
        />
      </div>

      <div>
        <label for="phone" class="form-label">Phone</label>
        <input
          type="tel"
          id="phone"
          bind:value={phone}
          class="form-input"
          placeholder="(555) 123-4567"
        />
      </div>

      {#if showSubject}
        <div>
          <label for="subject" class="form-label">Subject</label>
          <input
            type="text"
            id="subject"
            bind:value={subject}
            class="form-input"
            placeholder="Subject"
          />
        </div>
      {/if}

      <div>
        <label for="message" class="form-label">Message</label>
        <textarea
          id="message"
          bind:value={message}
          required
          rows="5"
          class="form-input resize-none"
          placeholder="Your message..."
        ></textarea>
      </div>

      <button
        type="submit"
        disabled={submitting}
        class="btn-primary w-full flex items-center justify-center gap-2"
      >
        {#if submitting}
          <i class="fa-solid fa-spinner animate-spin"></i>
          Sending...
        {:else}
          {submitButtonText}
        {/if}
      </button>
    </form>
  {/if}
</div>
