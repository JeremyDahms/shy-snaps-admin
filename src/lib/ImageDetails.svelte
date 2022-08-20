<script>
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    function submitImage(e) {
        const formData = new FormData(e.target);

        const data = {};
        for (let field of formData) {
            const [key, value] = field;
            data[key] = value;
        }
        console.log(data);
        fetch('http://localhost:8080/images', {
            method: 'POST',
            body: formData,
        })
    }

    function getImageData(e) {
        const files = e.srcElement.files[0];
        if (files) {
            const fileReader = new FileReader();
            fileReader.readAsDataURL(files);
            fileReader.addEventListener('load', function () {
                const dataUrl = this.result;
                dispatch('selectImageEvent', {
                    dataUrl
                });                
            })
        }
    }
</script>

<form on:submit|preventDefault={submitImage} id='theForm'>
    <div>
        <label for='image'>Choose Image</label>
        <input on:change={getImageData} type='file' accept='image/*' id='image' name='image' />
    </div>
    <div>
        <label for='title'>Title</label>
        <input type='text' id='title' name='title' value=''/>
    </div>
    <div>
        <label for='description'>Description</label>
        <input type='text' id='description' name='description' value=''/>
    </div>
    <div>
        <label for='tags'>Tags</label>
        <input type='text' id='tags' name='tags' value=''/>
    </div>
    <button type='submit'>Upload to SHY STUDIOS</button>
</form>

<style>
    form {
        display: flex;
        flex-direction: column;
    }
    form > div {
        display: flex;
        justify-content: space-between;
    }
    form > div + * {
        margin-top: 10px;
    }
</style>