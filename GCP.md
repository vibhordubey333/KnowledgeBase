1. To configure shell:<br/>
   `https://cloud.google.com/sdk/docs/install`<br/>
   
2. To initialize gcloud on terminal. <br/>
   `gcloud auth login` <br/>
   or<br/>
   `gcloud init --no-launch-browser`
   
3. To set project on terminal:<br/>
   `gcloud config set project [project-ID]`<br/>
   You can get all projects here: https://console.cloud.google.com/welcome/

4. To list compute:<br/>
   `gcloud compute instances list`<br/>

5. To SSH created VM in compute: `gcloud compute ssh <project-id> --zone <your-zone>`
   
4. To delete projects: <br/>
  Navigate to this page: https://console.cloud.google.com/cloud-resource-manager <br/>
  OR <br/>
  `gcloud projects delete [..your-project-id..]`<br/>
  
  #### To Create Buckets<br/><br/>
  ---
  
  1. Search for `Bucket`.<br/>
  2. Click on `Create Bucket`. Provide it a unique name globally.[All in lowercase]<br/>
  3. Opt for options as per use-case.<br/>
  4. Bucket is created.<br/>
  5. Create a folder inside bucket where we can store our image for instance.<br/>
  6. Upload programmatically[GO SDK] or by clicking on upload file button.<br/>
  
 
