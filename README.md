name: GitHub action dispath

on:
  workflow_dispatch:
    inputs:
      source_regurl_tag:
        required: true
        default: ""
        description: "Container image registry URL with tag. e.g., gcr.io/project-id-372417/source-image:2650c2f7c04640b8c67df560510914f7ba2033e2"
      target_regurl:
        required: true
        default: ""
        description: "Container image registry URL without tag. e.g., gcr.io/project-id-372417/target-image"

jobs:
  copy_container_image:
    name: Copy container image
    runs-on: ubuntu-latest
    env:
      IMAGE_TAG: ''
      TARGET_IMAGE: ''   
    steps:
      - name: print
        run: |
          echo ${{ inputs.source_regurl_tag }}
          echo ${{ inputs.target-tag }}
      - name: Get image tag
        run: |
          echo IMAGE_TAG=$(echo ${{ inputs.source_regurl_tag }} | cut -d":" -f2) >> $GITHUB_ENV
          echo "TARGET_IMAGE=${{ inputs.target_regurl }}:${{ env.IMAGE_TAG }}" >> $GITHUB_ENV

      - uses: 'google-github-actions/auth@v1'
        with:
          credentials_json: ${{ secrets.SA_A }}

      - name: Configure Docker auth for gcloud command-line
        run: gcloud --quiet auth configure-docker && gcloud auth list
      
      - name: Pull from source image
        run: docker pull ${{ inputs.source_regurl_tag }}

      - name: Tag target image
        run: docker tag ${{ inputs.source_regurl_tag }} ${{ inputs.target_regurl }}:${{ env.IMAGE_TAG }}

      - name: Push to target
        run: docker push ${{ inputs.target_regurl }}:${{ env.IMAGE_TAG }}

      - name: Summary
        run: |
          echo "source_regurl_tag: ${{ inputs.source_regurl_tag }}" >> $GITHUB_STEP_SUMMARY
          echo "target_regurl: ${{ inputs.target_regurl }}" >> $GITHUB_STEP_SUMMARY
          echo "TARGET_IMAGE: ${{ inputs.target_regurl }}:${{ env.IMAGE_TAG }}" >> $GITHUB_STEP_SUMMARY

      - uses: hmarr/debug-action@v2
        if: always()
