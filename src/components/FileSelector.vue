<template>
  <select
    v-model="selected"
    class="form-select mt-10 block w-full border-4 border-cyan-950 p-3 rounded mb-10"
  >
    <option value="0">Select File</option>
    <option v-for="(file, index) in files" :value="file" :key="index">
      {{ file.title }}
    </option>
  </select>

  <!-- Information Block -->
  <div class="grid md:grid-cols-1 gap-4 font-sans">
    <!-- Photo -->
    <div
      class="shadow-md bg-black p-10 text-center rounded mb-10"
      v-if="selected && selected.images"
    >
      <img
        v-if="selected && selected.images"
        :src="selected.images[0].thumb"
        alt="Selected Image"
        class="w-32 h-32 mt-4 mx-auto mb-10"
      />
      <!-- Subject -->
      <div class="text-lg mb-4">
        <span class="font-bold text-gray-500">-SUBJECT-</span>
        <p
          class="text-slate-100"
          v-if="selected && selected.subjects && selected.subjects.length > 0"
        >
          {{ selected.subjects[0] }}
        </p>
      </div>
      <!-- Description -->
      <div class="text-lg mb-4">
        <span class="font-bold text-gray-500">-DESCRIPTION-</span>
        <p class="text-slate-100 text-center">
          {{ selected.description }}
        </p>
      </div>
      <!-- WARNING -->
      <div
        class="text-lg mb-4"
        v-if="
          selected &&
          selected.warning_message &&
          selected.warning_message.length > 0
        "
      >
        <span class="font-bold text-rose-700"
          ><i class="fa-solid fa-triangle-exclamation"></i> WARNING!
        </span>
        <p class="text-rose-700">{{ selected.warning_message }}</p>
      </div>
      <!-- Reward -->
      <div
        class="text-lg mb-4 text-yellow-300 text-center font-bold"
        v-if="selected && selected.reward_text"
      >
        <i class="fa-solid fa-sack-dollar"></i> {{ selected.reward_text }}
      </div>
      <!-- More Information -->
      <div class="text-lg mb-4 text-slate-100">
        <a
          :href="selected.url"
          v-if="selected && selected.url"
          target="_blank"
          class="underline hover:bg-gray-700"
          >Click here for more information</a
        >
      </div>

      <!-- Publish Date -->
      <div class="text-bace mb-4">
        <p class="text-neutral-500">
          {{ selected.publication }}
        </p>
      </div>

      <!-- Contact -->
      <div class="text-bace mb-4 text-slate-700 italic">
        <p>
          If you have any information concerning this person, please contact
          your
          <a
            href="https://www.fbi.gov/contact-us/field-offices"
            target="_blank"
            class="underline hover:bg-cyan-500"
            >local FBI office</a
          >
          or the nearest
          <a
            href="https://www.fbi.gov/contact-us/legal-attache-offices"
            target="_blank"
            class="underline hover:bg-cyan-500"
            >American Embassy or Consulate</a
          >.
        </p>
      </div>
    </div>
    <!-- select case -->
    <div class="text-center text-3xl text-gray-400" v-else>
      <p>Please select a file to check the detail.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "FileSelector",
  props: ["files"],
  data() {
    return {
      selected: 0,
    };
  },
};
</script>
