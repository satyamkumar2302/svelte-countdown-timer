<script>
    import ProgressBar from "./ProgressBar.svelte";
    let secondsleft = 20;
    let isRunning = false;

    const startTimer = ()=>{
        const timer = setInterval(()=>{
            secondsleft-=1;
            isRunning=true;
            if(secondsleft<=0) {
                clearInterval(timer); 
                secondsleft=20;
                isRunning=false;
            }
        }, 1000);
    }

    $: progress = (20-secondsleft)/20*100;
    
</script>

<style>
    .start{
        background-color: rgb(154,73,73);
        width: 100%;
        margin: 10px 0;
    }

    .start[disabled]{
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>

<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondsleft}</h2>
</div>

<ProgressBar progress={progress}/>

<div bp="grid">
    <button class="start" bp="offset-5@md 4@md 12@sm" disabled={isRunning} on:click={startTimer}>Start</button>
</div>