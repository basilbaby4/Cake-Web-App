<script>
    let files;
    let dataFile = null;
    let name;
    let comment=null;
    function upload() {
        let valid  =   true;
        if(name.length>30){
            valid = false;
            alert('Name should not exceed 30 characters');
        }else if(comment.length>200){
            valid = false;
            alert('Comment should not exceed 200 characters');
        }
        if(valid){
            const formData = new FormData();
            formData.append('name', name);
            formData.append('comment', comment);
            formData.append('file', files[0]);
            const upload = fetch('http://localhost:3000/createCake', {
                method: 'POST',
                body: formData
            }).then((response) => response.json()).then((result) => {
                console.log('Success:', result);
                if(result.status==true){
                    alert(result.message);
                    window.location.href = '/';                
                }else{
                    alert(result.message);
                }
            }) .catch((error) => {
                console.error('Error:', error);
            });
        }

    
    }
</script>

<div class='container' style="margin-top:100px">

    <h3 class=''>

       Add New Cake 
        
    </h3>

<div class='row'>

    

    <form  method="get"  action='/'  on:submit|preventDefault={upload} >

    <div class="form-group">
        <label for="Name">Name:</label>
        <input required class='form-control' type="text" bind:value={name} /> 
    </div>

    <div class="form-group">
        <label for="Comment">Comment:</label>
        <textarea required class='form-control'  bind:value={comment}></textarea>
    </div>

    <br>

    <div class="form-group">
        <input required id="fileUpload" type="file" bind:files>
    </div>
    
    
 

 
 
    <div class="mt-3">

     <button  class='btn btn-primary'  >Submit</button>

    </div>
 
</form>

</div>

</div>
