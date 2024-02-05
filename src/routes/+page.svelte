<script lang="ts">
  import {onMount} from 'svelte'
  let form = {    
    name: "",
    country: "",
    email: "",
    password: "",
  };

  let localStorageData:any[]=[];

  function f(){
   for (let i=0;i<localStorage.length;i++){
    const key=localStorage.key(i);
    if(key){
      localStorageData.push(JSON.parse(localStorage.getItem(key)??''))
    }
   }
   localStorageData=localStorageData   
  }
  
  function submitForm() { 
    const nameInput = form.name.trim();
    
    if (nameInput === "") {  
      alert("Enter the name");
      return;
    }
    
    const countryInput = form.name.trim();
 
    if (countryInput === "") {
      alert("Enter the country name");
      return;
    }
    
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(form.email)) {
      alert("Email is not valid");
      return;
    }

    const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
    if (!passwordRegex.test(form.password)) {
      alert("Password is not valid");
      return;
    }

    console.log("Form submitted:", form);
    
    localStorage.setItem(form.email , JSON.stringify({ Name: form.name, Email: form.email, Country: form.country }));
  }

  onMount(()=>{
    f();
    console.log(localStorageData);
  })

  
    
</script>

<main class="min-h-screen flex items-center justify-center bg-[#f1e7f8]">
  <div class="bg-[#e9e1f8] p-8 rounded-lg">
    <div class="mb-4">
      <label class="text-sm font-medium text-gray-600" for="name">
        Name:
      </label>
      <input
        class="mt-1 p-2 w-full border rounded-md"
        id="name"
        type="text"
        bind:value={form.name}
      />
    </div>

    <div class="mb-4">
      <label class="text-sm font-medium text-gray-600" for="country">
        Country:
      </label>
      <input
        class="mt-1 p-2 w-full border rounded-md"
        id="country"
        type="text"
        bind:value={form.country}
      />
    </div>

    <div class="mb-4">
      <label class="text-sm font-medium text-gray-600" for="email">
        Email:
      </label>
      <input
        class="mt-1 p-2 w-full border rounded-md"
        id="email"
        type="email"
        bind:value={form.email}
      />
    </div>

    <div class="mb-4">
      <label class="text-sm font-medium text-gray-600" for="password">
        Password:
      </label>
      <input
        class="mt-1 p-2 w-full border rounded-md"
        id="password"
        type="password"
        bind:value={form.password}
      />
    </div>

    <button
      class="w-full bg-black text-white px-3 py-2 rounded-md font-serif font-bold hover:bg-gray-800"
      on:click={submitForm}
    >
      Submit
    </button>

  </div>
</main>
  <div class="flex justify-center bg-[#f1e7f8]">
    <table class="bg-[#e9e1f8] border-gray-300 w-[70] mb-20">
        <thead>
            <tr>
                <th class="py-2 px-4 border-b">Name</th>
                <th class="py-2 px-4 border-b">Country</th>
                <th class="py-2 px-4 border-b">Email</th>
            </tr>
        </thead>
            <tbody>
              {#if localStorageData.length>0}
              {#each localStorageData as data}
              <tr>
                <td class="py-2 px-4 border-b">{data.Name}</td>
                <td class="py-2 px-4 border-b">{data.Country}</td>
                <td class="py-2 px-4 border-b">{data.Email}</td>
              </tr>
              {/each}
              {/if}
            </tbody>
    </table>
  </div>
