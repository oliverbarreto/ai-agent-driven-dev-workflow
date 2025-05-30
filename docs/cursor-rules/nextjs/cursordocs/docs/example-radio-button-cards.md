# Example

```typescript
<div
  role="radiogroup"
  aria-required="false"
  dir="ltr"
  class="grid grid-cols-3 gap-4"
  tabindex="0"
  style="outline:none"
>
  <div>
    <button
      type="button"
      role="radio"
      aria-checked="true"
      data-state="checked"
      value="card"
      class="aspect-square h-4 w-4 rounded-full border border-primary text-primary shadow focus:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:cursor-not-allowed disabled:opacity-50 peer sr-only"
      id="card"
      aria-label="Card"
      tabindex="-1"
      data-radix-collection-item=""
    >
      <span data-state="checked" class="flex items-center justify-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-circle h-3.5 w-3.5 fill-primary"
        >
          <circle cx="12" cy="12" r="10"></circle>
        </svg>
      </span>
    </button>
    <label
      class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70 flex flex-col items-center justify-between rounded-md border-2 border-muted bg-transparent p-4 hover:bg-accent hover:text-accent-foreground peer-data-[state=checked]:border-primary [&amp;:has([data-state=checked])]:border-primary"
      for="card"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        class="mb-3 h-6 w-6"
      >
        <rect width="20" height="14" x="2" y="5" rx="2"></rect>
        <path d="M2 10h20"></path>
      </svg>
      Card
    </label>
  </div>
  <div>
    <button
      type="button"
      role="radio"
      aria-checked="false"
      data-state="unchecked"
      value="paypal"
      class="aspect-square h-4 w-4 rounded-full border border-primary text-primary shadow focus:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:cursor-not-allowed disabled:opacity-50 peer sr-only"
      id="paypal"
      aria-label="Paypal"
      tabindex="-1"
      data-radix-collection-item=""
    ></button>
    <label
      class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70 flex flex-col items-center justify-between rounded-md border-2 border-muted bg-transparent p-4 hover:bg-accent hover:text-accent-foreground peer-data-[state=checked]:border-primary [&amp;:has([data-state=checked])]:border-primary"
      for="paypal"
    >
      <svg role="img" viewBox="0 0 24 24" class="mb-3 h-6 w-6">
        <path
          d="M7.076 21.337H2.47a.641.641 0 0 1-.633-.74L4.944.901C5.026.382 5.474 0 5.998 0h7.46c2.57 0 4.578.543 5.69 1.81 1.01 1.15 1.304 2.42 1.012 4.287-.023.143-.047.288-.077.437-.983 5.05-4.349 6.797-8.647 6.797h-2.19c-.524 0-.968.382-1.05.9l-1.12 7.106zm14.146-14.42a3.35 3.35 0 0 0-.607-.541c-.013.076-.026.175-.041.254-.93 4.778-4.005 7.201-9.138 7.201h-2.19a.563.563 0 0 0-.556.479l-1.187 7.527h-.506l-.24 1.516a.56.56 0 0 0 .554.647h3.882c.46 0 .85-.334.922-.788.06-.26.76-4.852.816-5.09a.932.932 0 0 1 .923-.788h.58c3.76 0 6.705-1.528 7.565-5.946.36-1.847.174-3.388-.777-4.471z"
          fill="currentColor"
        ></path>
      </svg>
      Paypal
    </label>
  </div>
  <div>
    <button
      type="button"
      role="radio"
      aria-checked="false"
      data-state="unchecked"
      value="apple"
      class="aspect-square h-4 w-4 rounded-full border border-primary text-primary shadow focus:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:cursor-not-allowed disabled:opacity-50 peer sr-only"
      id="apple"
      aria-label="Apple"
      tabindex="-1"
      data-radix-collection-item=""
    ></button>
    <label
      class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70 flex flex-col items-center justify-between rounded-md border-2 border-muted bg-transparent p-4 hover:bg-accent hover:text-accent-foreground peer-data-[state=checked]:border-primary [&amp;:has([data-state=checked])]:border-primary"
      for="apple"
    >
      <svg role="img" viewBox="0 0 24 24" class="mb-3 h-6 w-6">
        <path
          d="M12.152 6.896c-.948 0-2.415-1.078-3.96-1.04-2.04.027-3.91 1.183-4.961 3.014-2.117 3.675-.546 9.103 1.519 12.09 1.013 1.454 2.208 3.09 3.792 3.039 1.52-.065 2.09-.987 3.935-.987 1.831 0 2.35.987 3.96.948 1.637-.026 2.676-1.48 3.676-2.948 1.156-1.688 1.636-3.325 1.662-3.415-.039-.013-3.182-1.221-3.22-4.857-.026-3.04 2.48-4.494 2.597-4.559-1.429-2.09-3.623-2.324-4.39-2.376-2-.156-3.675 1.09-4.61 1.09zM15.53 3.83c.843-1.012 1.4-2.427 1.245-3.83-1.207.052-2.662.805-3.532 1.818-.78.896-1.454 2.338-1.273 3.714 1.338.104 2.715-.688 3.559-1.701"
          fill="currentColor"
        ></path>
      </svg>
      Apple
    </label>
  </div>
</div>
```
