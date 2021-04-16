<script>
    export let id; // UNDEFINED
	const fetchImage = (async () => {
        try {
		const response = await fetch('http://localhost:3000/?id='+id)
        return await response.json();
        }catch (err){
        }
	})()
</script>
<div class='container' style="margin-top:100px">
<div class='row'>
	{#await fetchImage}
	<p>...waiting</p>
{:then data}
<h5><a class="link-dark" style="font-size:14px" href="/">Back</a></h5>
<div class="col-lg-3">
	<img  class="img-fluid img-rounded" alt=''  src="http://localhost:3000/{data.data.imageUrl}"  /></div>
<div class="col-lg-9">
	<h5>{data.data.name} 		
 			 <span class="badge badge-primary" style="color: #fff;background-color: #007bff;">yumFactor : {data.data.yumFactor}</span>
 	</h5>
	<p>{data.data.comment}</p>
</div> 
{:catch error}
	<p>An error occurred!</p>
{/await}
</div>
</div>

