<script>
	const fetchImage = (async () => {
        try {
		const response = await fetch('http://localhost:3000/')
        return await response.json();
        }catch (err){

        }
	})();

    function handleClick(id) {


        var r = confirm("Are you sure you want to delete it?");
            if (r == true) {
                const deleteData = fetch('http://localhost:3000/deleteCake?id='+id, {
                method: 'DELETE'           
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

{#await fetchImage}
	<p>...waiting</p>
{:then data}
<div class='container' style="margin-top:100px">
    <h3 class=''>
        Cake List
        <a class="btn btn-info" style="float: right;" href="/create">Add New
        </a>
    </h3>
    <div class='row'>

        {#if data.data.length==0}
            <div class="alert alert-primary" role="alert">
               No records found.
            </div>
        {/if}

       

        {#each data.data as item}
        <div class=" col-lg-3 col-md-4 col-6 " style="border: 1px solid rgba(0,0,0,.125);">
            <a href="/cake/{item.id} "> 
                <img  src="http://localhost:3000/{item.imageUrl}" alt='' class="img-fluid img-rounded " style="margin-top: 10px;" >
            </a>
        <div class="card-body">
            <h5 class="card-title"><a href="/cake/{item.id} "> {item.name} </a></h5>
            <button class="btn btn-danger" on:click={() => handleClick(item.id)}>
                Delete
            </button>
        </div>
        </div> 
        {/each}
    </div>
</div>
{:catch error}
	<p>An error occurred!</p>
{/await}