# Larger files upload rejection message instead of net::ERR_CONNECTION_RESET

> Issue #28876 - Created on 4/19/2024

> Original URL: https://github.com/facebook/react/issues/28876

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:18.0.0

## Steps To Reproduce

1. Currently in my project if i try to upload larger files (mp3) the react app gives message in console ```net::ERR_CONNECTION_RESET``` and when i check inside network tab for the reason of failing this request its saying 400 bad request, and that's it. I tried to debug the app via chrome extension using vscode but no where it suggested the failing reason is due to file size issue. I think we should give some clear message or hint of file size in case it is the issue while file uploading. This software is proprietary. I will try to give show minimum reproducible env. here

I have a react component called Audiouploadwidget.tsx. This is simple function as here. The above function got hit when through user interface a user tries to upload a file
```
    function onUpload(event:any) {
        event.preventDefault()
        setDeleted(0)
        uploadAudio(files[0]);
    }
```
Next, i have BookDetails.tsx inside which is responsible for uploading audio files
 as here, it got hit during debugging as below.
```
  function handleUploadAudioAr(file: Blob) {
    uploadAudioAr(file);
  }
```
Then i have bookStore.ts, i am using Mobx, it got hit next during debugging.
```
  uploadAudioAr = async (file: any) => {
        this.uploadedAudioAr = 0
        this.uploadingAudioAr = true;
        try {
            const response = await agent.Media.create(file);
            const medium : MediumFormValues = response.data;
            runInAction(() => {
                this.currentAudioAr = (medium.md_ID) ? medium.md_ID : "00000000-0000-0000-0000-000000000000";
                if (this.selectedBook) {
                    this.selectedBook.md_AudioAr_ID = this.currentAudioAr;
                }
                this.srcAudioAr = ''; 
                this.srcAudioAr = this.srcAudioAr.concat('data:',medium.md_FileType,';base64,',medium.md_Medium);
                this.uploadedAudioAr = 1;
                this.uploadingAudioAr = false;
            })
        } catch (error) {
            console.log(error);
            runInAction(() => {
                this.uploadedAudioAr = -1
                this.uploadingAudioAr = false
            });
        }
    }
```
Then the request passes to agent.ts as below
```
    create: (file: any) => {
        let formData = new FormData();
        formData.append('Md_Medium', file);
        formData.append('Md_Title', "Title");
        formData.append('Md_Title_Ar', "Title Ar");
        return axios.post<MediumFormValues>('Medium/createMedium/', formData, {
            headers: { 'Content-Type': 'multipart/form-data' }
        })
    },
```
it is responsible for creating post request for Medium endpoint.
Then it goes to BookDetails.tsx where i have yup validations and useEffects, pass through these as below.
```
  const validationSchema = Yup.object().shape({
    bk_Code: Yup.string().required('Code required!').min(3, 'Minimum 3 characters required!'),
    bk_Name: Yup.string().required('Name required!').min(3, 'Minimum 3 characters required!'),
    bk_Name_Ar: Yup.string().required('Arabic Name required!').min(3, 'Minimum 3 characters required!'),
    bk_Title: Yup.string().required('Title required!').min(3, 'Minimum 3 characters required!'),
    bk_Title_Ar: Yup.string().required('Arabic Title required!').min(3, 'Minimum 3 characters required!')
  })

  useEffect(() => {
    if (id) loadBook(id).then(book => setBook(new BookFormValues(book)))
  }, [id, loadBook])

  useEffect(() => {
    loadAuthors();
  }, [loadAuthors])
and son on...
```
Then on continue hitting F5, i am using axios to send request. It goes to error block as defined here.
```
axios.interceptors.response.use(async response => {
    //if (process.env.NODE_ENV === 'development') await sleep(1000);
    const pagination = response.headers['pagination'];
    if (pagination) {
        response.data = new PaginatedResult(response.data, JSON.parse(pagination));
        return response as AxiosResponse<PaginatedResult<any>>
    }
    return response;
}, (error: AxiosError) => {
    const { data, status, config } = error.response as AxiosResponse;
```
and the message from above is ```TypeError: Cannot destructure property 'data' of 'error.response' as it is undefined.```
Further, it goes to line 424 in my agent.ts. Relevant part of the code is below.
```
        return axios.post<MediumFormValues>('Medium/createMedium/', formData, {
            headers: { 'Content-Type': 'multipart/form-data' }
        })

``` and just gives the error message ```net::ERR_CONNECTION_RESET```
I think it could be more explicit for the users who wants to upload the files which is more than the certain specific limit instead of message ```net::ERR_CONNECTION_RESET```.



<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
Sandboxed example could not be created as it is proprietary software
-->

## The current behavior
No message for file size

## The expected behavior
Explicit message for file size upload failure should be there instead of ```net::ERR_CONNECTION_RESET```

