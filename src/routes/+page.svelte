<script>
    let tanggal = ''
    // simpan tanggal di localStorage
    const saveTanggal = () => {
        localStorage.setItem('tanggal', tanggal)
        console.log(localStorage.getItem('tanggal'))
    }
</script>

<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-10">
			<h3 class="text-center mt-5">Home</h3>
           
		</div>
		<div class="col-md-5 text-center">
			<div class="d-flex form-group">
				<input type="text" class="form-control" placeholder="Tanggal Datang Tabung" bind:value={tanggal} />
                <button class="btn btn-primary" on:click={saveTanggal}>Simpan</button>
			</div>
		</div>
	</div>
</div>
