<template>
  <section class="subscibe-section section-space-sm">
            <div class="container">
                <div class="join-form-wrap">
                    <div class="row g-gs align-items-center">
                        <div class="col-lg-3">
                            <h3 class="form-title">{{ SectionData.newsletterData.title }}</h3>
                        </div><!-- end col -->
                       <div class="row mt-3">
                                                <div class="col-lg-6">
                                                    <label class="mb-2 form-label">Starting date</label>
                                                    <input type="date" class="form-control form-control-s1">
                                                </div><!-- end col-lg-6 -->
                                                <div class="col-lg-6">
                                                    <label class="mb-2 form-label">Expiration date</label>
                                                    <input type="date" class="form-control form-control-s1">
                                                </div><!-- end col-lg-6 -->
                                            </div><!-- end row -->
                        <div class="col-lg-3 col-md-4">
                            <a href="#" class="btn btn-primary d-md-block">{{ SectionData.newsletterData.btnText }}</a>
                        </div><!-- end col -->
                    </div><!-- row -->
                </div><!-- end join-form-wrap -->
            </div><!-- end container -->
    </section><!-- end subscibe-section -->
</template>

<script>
// Import component data. You can change the data in the store to reflect in all component
import SectionData from '@/store/store.js'

export default {
  name: 'Newsletter',
  data () {
    return {
      SectionData
    }
  }
}
</script>
