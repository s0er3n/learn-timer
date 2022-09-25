<script lang="ts">
    import {browser} from "$app/environment"
	let time = 90 * 60 * 1000; // 90 minutes



    let intervall: ReturnType<typeof setInterval>
    
    if (browser && Notification.permission !== "granted") {
        Notification.requestPermission()
    }
    const startIntervall = () => {
        clearInterval(intervall);
		intervall = setInterval(() => {
			time -= 1000;
            if (Math.random() < 1/120 ) {
                new Notification("chill")
            }
            if (Math.random() < 1/(60 *30)) {

                new Notification("reward")
            }
		}, 1000);
    }
	const startTimer = () => {
		time = 90 * 60 * 1000; // 90 minutes

        startIntervall()
	};
    const pause = () => {
        clearInterval(intervall);
    }
</script>

<button on:click={startTimer}>start timer</button>
<button on:click={pause}>pause timer</button>
<button on:click={startIntervall}>unpause timer</button>
{Math.floor(time/1000/60)}
{Math.floor(time/1000 % 60)}
