<script>
    // get current time
    import { onMount } from 'svelte';

    let time;
    let hours;
    let minutes;

    const updateTime = () => {
        time = new Date();
        const gmtPlus8 = new Date(time.getTime() + (8 * 60 * 60 * 1000));
        hours = gmtPlus8.getUTCHours() % 12 || 12;
        minutes = gmtPlus8.getUTCMinutes();
        if (minutes < 10) {
            minutes = '0' + minutes;
        }
    };

    onMount(() => {
        updateTime();
        const interval = setInterval(updateTime, 1000);
        return () => clearInterval(interval);
    });
</script>

<div class="grid place-items-center min-h-svh">
    <p class="text-3xl font-bold">{hours}:{minutes}</p>
</div>