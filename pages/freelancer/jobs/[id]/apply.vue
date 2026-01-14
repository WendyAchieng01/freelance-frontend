<template>
  <div>
    <p class="text-h5">Apply For This Job</p>
    <p class="text-subtitle-1 text-medium-emphasis mt-2">
      To apply for the job, you must fill in all the fields and submit to the
      client
    </p>

    <v-divider class="my-4" opacity="0.05" />

    <p class="text-h6">Job Description</p>

    <v-card flat class="mt-5">
      <!-- job title -->
      <div class="d-flex justify-space-between">
        <div>
          <p class="text-caption text-medium-emphasis">
            {{ moment(currentJob?.posted_date).fromNow() }}
            <v-icon icon="mdi-circle-small" />
            {{ currentJob?.current_applications_count }} Bids
          </p>
          <p class="text-h6">
            {{ currentJob?.title }}
          </p>
          <p class="text-caption text-medium-emphasis text-capitalize">
            {{ currentJob?.preferred_freelancer_level }} Level
            <v-icon icon="mdi-circle-small" />
            {{ formatAmount(currentJob?.price ?? 0) }}
            <v-icon icon="mdi-circle-small" />
            {{
              moment(currentJob?.deadline_date).diff(
                currentJob?.posted_date,
                "days"
              )
            }}
            days
          </p>
        </div>
      </div>

      <!-- job description -->
      <p class="mt-4 text-subtitle-1">
        {{ currentJob?.description }}
      </p>

      <!-- deadline and client rating -->
      <div class="d-flex ga-3 mt-5 text-medium-emphasis">
        <p class="text-subtitle-1">
          Deadline: {{ moment(currentJob?.posted_date).format("Do MMMM YYYY") }}
        </p>
      </div>
    </v-card>

    <!-- training materials -->
    <!-- <p class="text-subtitle-1 mt-10">Training Materials</p>
    <p class="text-subtitle-1 text-medium-emphasis border pa-2 w-50 rounded">
      www.materials.com
    </p> -->

    <!-- skills required -->
    <div class="mt-10">
      <p class="text-subtitle-1">Skills required</p>
      <div class="d-flex ga-2 mt-5">
        <v-chip
          v-for="skill in currentJob?.skills_required_display"
          :key="skill.id"
          :text="skill.name"
          class="text-medium-emphasis text-capitalize"
        />
      </div>
    </div>

    <!-- application form -->
    <p class="text-h6 mt-10">Kindly fill the form correctly</p>
    <v-form ref="formElement" class="mt-5" @submit.prevent="submitApplication">
      <template #default="{ isValid }">
        <div class="upload-section mt-6">
          <p class="text-subtitle-1 font-weight-medium mb-4 primary--text">
            Required Application Documents
          </p>
          <p class="text-body-2 grey--text text--darken-1 mb-6">
            Please upload clear, up-to-date files. PDF format is strongly preferred.
            Max file size: 10MB per document.
          </p>

          <v-row dense>
            <!-- CV - Most important, put first -->
            <v-col cols="12" sm="6">
              <v-file-input
                v-model="applicationForm.cv"
                label="Curriculum Vitae (CV) *"
                hint="PDF preferred • Max 10MB • Include relevant experience & skills"
                persistent-hint
                prepend-icon="mdi-file-account"
                accept=".pdf,.doc,.docx"
                show-size
                :rules="[
                  required,
                  v => !v || v.size <= 10 * 1024 * 1024 || 'File too large (max 10MB)',
                  v => !v || ['application/pdf', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document']
                    .includes(v.type) || 'Only PDF, DOC or DOCX allowed'
                ]"
                :error-messages="applicationFormErrors.cv || []"
                density="compact"
                class="mb-2"
              />
            </v-col>

            <!-- Cover Letter -->
            <v-col cols="12" sm="6">
              <v-file-input
                v-model="applicationForm.cover_letter"
                label="Cover Letter *"
                hint="PDF preferred • Tell us why you're perfect for this job (1-2 pages)"
                persistent-hint
                prepend-icon="mdi-file-document-edit"
                accept=".pdf,.doc,.docx"
                show-size
                :rules="[
                  required,
                  v => !v || v.size <= 10 * 1024 * 1024 || 'File too large (max 10MB)',
                  v => !v || ['application/pdf', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document']
                    .includes(v.type) || 'Only PDF, DOC or DOCX allowed'
                ]"
                :error-messages="applicationFormErrors.cover_letter || []"
                density="compact"
                class="mb-2"
              />
            </v-col>

            <!-- Portfolio (optional but very important in creative/tech) -->
            <v-col cols="12">
              <v-file-input
                v-model="applicationForm.portfolio"
                label="Portfolio / Work Samples (Optional)"
                hint="PDF, images, or ZIP • Showcase your best relevant work (max 10MB)"
                persistent-hint
                prepend-icon="mdi-briefcase-variant"
                accept=".pdf,.zip,.jpg,.jpeg,.png,.doc,.docx"
                multiple
                show-size
                :rules="[
                  v => !v || v.every(file => file.size <= 10 * 1024 * 1024) || 'Each file must be under 10MB',
                  v => !v || v.every(file => 
                    ['application/pdf','application/zip','image/jpeg','image/png',
                    'application/msword','application/vnd.openxmlformats-officedocument.wordprocessingml.document']
                    .includes(file.type)) || 'Allowed: PDF, ZIP, JPG, PNG, DOC, DOCX'
                ]"
                :error-messages="applicationFormErrors.portfolio || []"
                density="compact"
              >
                <template v-slot:selection="{ fileNames }">
                  <v-chip
                    v-for="(fileName, i) in fileNames"
                    :key="i"
                    color="primary"
                    label
                    small
                    class="ma-1"
                  >
                    {{ fileName }}
                  </v-chip>
                </template>
              </v-file-input>
            </v-col>
          </v-row>

          <!-- Quick tips / preview -->
          <v-alert
            v-if="applicationForm.cv || applicationForm.cover_letter"
            type="info"
            variant="tonal"
            density="compact"
            class="mt-4"
            icon="mdi-lightbulb-outline"
          >
            Good applications with clear CVs + tailored cover letters get 3× more responses!
          </v-alert>
        </div>

        <!-- payment details -->
        <p class="text-h6">Payment Details</p>
        <v-row class="mt-5">
          <v-col cols="5">
            <p class="text-subtitle-1">Price</p>
            <p class="text-subtitle-2">
              This is the total amount the client is offering for the job
            </p>
          </v-col>
          <v-col>
            <v-text-field
              readonly
              :model-value="formatAmount(currentJob?.price ?? 0)"
              class="w-sm-50"
            />
          </v-col>
        </v-row>
        <v-row class="mt-5">
          <v-col cols="5">
            <p class="text-subtitle-1">5% Freelancer Fee</p>
          </v-col>
          <v-col>
            <v-text-field
              disabled
              :model-value="
                formatAmount(
                  parseFloat(!!currentJob?.price ? currentJob.price : '0') *
                    0.05
                )
              "
              class="w-sm-50"
            />
          </v-col>
        </v-row>
        <v-row class="mt-5">
          <v-col cols="5">
            <p class="text-subtitle-1">You will get</p>
          </v-col>
          <v-col>
            <v-text-field
              readonly
              :model-value="
                formatAmount(
                  parseFloat(currentJob?.price ?? '0') -
                    parseFloat(!!currentJob?.price ? currentJob.price : '0') *
                      0.05
                )
              "
              class="w-sm-50"
            />
          </v-col>
        </v-row>

        <!-- actions -->
        <v-btn
          text="Apply Now"
          size="x-large"
          class="text-subtitle-1"
          type="submit"
          :loading
          :disabled="!isValid.value"
        />
        <v-btn
          text="Cancel"
          size="x-large"
          variant="text"
          class="text-subtitle-1"
          :to="`/freelancer/jobs/${currentJob?.slug}`"
        />
      </template>
    </v-form>

    <!-- success modal -->
    <AppModal
      v-model="showSuccessModal"
      message="You have succesfully applied for this job"
      @closed="redirectToDashboard"
      @action-click="redirectToDashboard"
    />
  </div>
</template>

<script setup lang="ts">
import moment from "moment";
import { useAppStore } from "~/store/app";
import { useFreelancerJobsStore } from "~/store/freelancer/jobs";
import { useFreelancerTrainingsStore } from "~/store/freelancer/trainings";
import type { IJobApplicationCreatePayload } from "~/types/freelancer";

definePageMeta({
  layout: "freelancer",
});

const jobStore = useFreelancerJobsStore();
const { currentJob, isLoading: loading } = storeToRefs(jobStore);
const trainingsStore = useFreelancerTrainingsStore();
const appStore = useAppStore();

const route = useRoute();
onMounted(async () => {
  await jobStore
    .fetchJobDetails(route.params.id as string)
    .then(async (job) => {
      await trainingsStore.fetchTrainingsForJob(job.slug);
    });
});

const formElement = useTemplateRef("formElement");
const {
  form: applicationForm,
  errors: applicationFormErrors,
  setErrors: setApplicationErrors,
  reset: resetApplicationErrors,
} = useForm<IJobApplicationCreatePayload>({
  portfolio: null,
  cover_letter: null,
  cv: null,
});

const showSuccessModal = ref(false);
async function submitApplication() {
  formElement.value?.resetValidation();
  if (currentJob.value?.has_applied) {
    appStore.showSnackBar({
      type: "info",
      message: "You have already applied for this job.",
    });
    return;
  }

  try {
    if (!currentJob.value) throw new Error("currentJob is not set");
    await jobStore.applyForJob(
      currentJob.value.slug,
      toFormData(applicationForm as Record<string, any>)
    );
    showSuccessModal.value = true;
    setTimeout(() => redirectToDashboard(), 3000);
    resetApplicationErrors();
    formElement.value?.reset();
  } catch (error: any) {
    console.log("Error while applying to job", error);
    const applicationBackendErrors = error.response?._data;
    if (applicationBackendErrors) {
      setApplicationErrors(applicationBackendErrors);
      const generalErrorMessage =
        applicationBackendErrors.detail ||
        applicationBackendErrors.non_field_errors?.[0] ||
        "Failed to post job. Please check your inputs.";
      appStore.showSnackBar({ type: "error", message: generalErrorMessage });
    }
  }
}

function redirectToDashboard() {
  showSuccessModal.value = false;
  // this will prevent from double redirection since when the user selects 'Okay' the dialog will close and emit the closed event
  const path = "/freelancer/dashboard";
  if (route.path !== path) {
    navigateTo(path);
  }
}
</script>
