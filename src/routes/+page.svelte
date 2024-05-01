<!-- Piano.svelte -->
<script lang="ts">
	import { keyMap } from '$lib/keyMap';
	const keys = [
		{ note: 'C3', keyCode: 'C3' },
		{ note: 'C#3', keyCode: 'Db3' },
		{ note: 'D3', keyCode: 'D3' },
		{ note: 'D#3', keyCode: 'Eb3' },
		{ note: 'E3', keyCode: 'E3' },
		{ note: 'F3', keyCode: 'F3' },
		{ note: 'F#3', keyCode: 'Gb3' },
		{ note: 'G3', keyCode: 'G3' },
		{ note: 'G#3', keyCode: 'Ab3' },
		{ note: 'A3', keyCode: 'A3' },
		{ note: 'A#3', keyCode: 'Bb3' },
		{ note: 'B3', keyCode: 'B3' },
		{ note: 'C4', keyCode: 'C4' }, // Second octave
		{ note: 'C#4', keyCode: 'Db4' },
		{ note: 'D4', keyCode: 'D4' },
		{ note: 'D#4', keyCode: 'Eb4' },
		{ note: 'E4', keyCode: 'E4' },
		{ note: 'F4', keyCode: 'F4' },
		{ note: 'F#4', keyCode: 'Gb4' },
		{ note: 'G4', keyCode: 'G4' },
		{ note: 'G#4', keyCode: 'Ab4' },
		{ note: 'A4', keyCode: 'A4' },
		{ note: 'A#4', keyCode: 'Bb4' },
		{ note: 'B4', keyCode: 'B4' },
		{ note: 'C5', keyCode: 'C5' }, // Third octave
		{ note: 'C#5', keyCode: 'Db5' },
		{ note: 'D5', keyCode: 'D5' },
		{ note: 'D#5', keyCode: 'Eb5' },
		{ note: 'E5', keyCode: 'E5' },
		{ note: 'F5', keyCode: 'F5' },
		{ note: 'F#5', keyCode: 'Gb5' },
		{ note: 'G5', keyCode: 'G5' },
		{ note: 'G#5', keyCode: 'Ab5' },
		{ note: 'A5', keyCode: 'A5' },
		{ note: 'A#5', keyCode: 'Bb5' },
		{ note: 'B5', keyCode: 'B5' },
		{ note: 'C6', keyCode: 'C6' }
	];

	const keyFrequencies = {
		C3: { frequency: 130.81 }, // C3
		Db3: { frequency: 138.59 }, // C#3/Db3
		D3: { frequency: 146.83 }, // D3
		Eb3: { frequency: 155.56 }, // D#3/Eb3
		E3: { frequency: 164.81 }, // E3
		F3: { frequency: 174.61 }, // F3
		Gb3: { frequency: 185.0 }, // F#3/Gb3
		G3: { frequency: 196.0 }, // G3
		Ab3: { frequency: 207.65 }, // G#3/Ab3
		A3: { frequency: 220.0 }, // A3
		Bb3: { frequency: 233.08 }, // A#3/Bb3
		B3: { frequency: 246.94 }, // B3
		C4: { frequency: 261.63 }, // C4
		Db4: { frequency: 277.18 }, // C#4/Db4
		D4: { frequency: 293.66 }, // D4
		Eb4: { frequency: 311.13 }, // D#4/Eb4
		E4: { frequency: 329.63 }, // E4
		F4: { frequency: 349.23 }, // F4
		Gb4: { frequency: 369.99 }, // F#4/Gb4
		G4: { frequency: 392.0 }, // G4
		Ab4: { frequency: 415.3 }, // G#4/Ab4
		A4: { frequency: 440.0 }, // A4
		Bb4: { frequency: 466.16 }, // A#4/Bb4
		B4: { frequency: 493.88 }, // B4
		C5: { frequency: 523.25 }, // C5
		Db5: { frequency: 554.37 }, // C#5/Db5
		D5: { frequency: 587.33 }, // D5
		Eb5: { frequency: 622.25 }, // D#5/Eb5
		E5: { frequency: 659.26 }, // E5
		F5: { frequency: 698.46 }, // F5
		Gb5: { frequency: 739.99 }, // F#5/Gb5
		G5: { frequency: 783.99 }, // G5
		Ab5: { frequency: 830.61 }, // G#5/Ab5
		A5: { frequency: 880.0 }, // A5
		Bb5: { frequency: 932.33 }, // A#5/Bb5
		B5: { frequency: 987.77 }, // B5
		C6: { frequency: 1046.5 } // C6
	};

	function playSound(event) {
		const { keyCode } = event;
		console.log(keyCode);
		const key = keys.find((key) => key.keyCode === keyCode);
		console.log(key);
		if (key) {
			const { frequency } = keyFrequencies[key.keyCode];
			const flooredFrequency = Math.floor(frequency);
			// const note = encodeURIComponent(key.note.replace('#', '%23')); // Encode '#' character
			console.log(`sounds/${flooredFrequency}.mp3`);
			const audio = new Audio(`sounds/${flooredFrequency}${key.keyCode}.mp3`);
			audio.play();
		}
	}

	// Function to handle key press event
	function handleKeyPress(event) {
		if (event.key === 'Shift') {
			console.log('ahahahhaha Shift pressed');
			// Check if it's the left shift key
			if (event.location === 1) {
				console.log('Left Shift pressed');
				// Handle left shift press
        const keyCode = keyMap['shiftLeft'];
        if (keyCode) {
          playSound({ keyCode });
        }
			} else if (event.location === 2) {
				console.log('Right Shift pressed');
				// Handle right shift press
			}
			const shiftPressed = true;
		} else if (event.key === 'Backspace') {
			console.log('Backspace pressed');
			// Handle backspace press
      const keyCode = keyMap['backspace'];
			if (keyCode) {
				playSound({ keyCode });
			}
		} else {
			// Handle other keys
			const keyPressed = event.key.toLowerCase();
			console.log(keyPressed);
			const keyCode = keyMap[keyPressed];
      console.log(`Key pressed: ${event.key}, KeyCode: ${keyCode}`);
			if (keyCode) {
				playSound({ keyCode });
			}
		}
	}

	import { onMount } from 'svelte';
	onMount(() => {
		window.addEventListener('keydown', handleKeyPress);
	});
</script>

{#each keys as { note, keyCode }}
	<button class="key" on:keypress={handleKeyPress} on:click={() => playSound({ keyCode })}
		>{note}</button
	>
{/each}

<style>
	.key {
		display: inline-block;
		width: 50px;
		height: 150px;
		margin: 5px;
		border: 1px solid black;
		text-align: center;
		line-height: 150px;
		font-size: 24px;
		cursor: pointer;
	}
</style>
