<script>
    import { importData } from 'src/js/importer';
    import { generatePages } from 'src/js/pages';
    import { text } from 'src/js/store';
    import { setSelection } from 'src/js/textarea';

    import Button from 'src/components/Button';

    let input;
    let files;

    const handleInput = async () => {
        const file = files[0];

        if (file) {
            const extension = file.name.split('.').pop();
            if (extension === 'md') {
                $text = await file.text();
            } else {
                const buffer = await file.arrayBuffer();
                const data = new Uint8Array(buffer);
                importData(data);
            }
            generatePages();
            setSelection(0);
        }
    };
</script>

<Button
    on:click={() => { input.click() }}
    tertiary
    animate
    customPadding="p-2"
>
    <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" d="M6 2a2 2 0 00-2 2v12a2 2 0 002 2h8a2 2 0 002-2V7.414A2 2 0 0015.414 6L12 2.586A2 2 0 0010.586 2H6zm5 6a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V8z" clip-rule="evenodd"/>
    </svg>
    <input
        bind:this={input}
        bind:files
        on:change={handleInput}
        accept=".md, .bkd"
        type="file"
        class="
        hidden
    ">
</Button>
