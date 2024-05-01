<!-- Piano.svelte -->
<script lang="ts">
	const keys = [
		{ note: 'C3', keyCode: 'C3' },
		{ note: 'C#3', keyCode: 'C#3' },
		{ note: 'D3', keyCode: 'D3' },
		{ note: 'D#3', keyCode: 'D#3' },
		{ note: 'E3', keyCode: 'E3' },
		{ note: 'F3', keyCode: 'F3' },
		{ note: 'F#3', keyCode: 'F#3' },
		{ note: 'G3', keyCode: 'G3' },
		{ note: 'G#3', keyCode: 'G#3' },
		{ note: 'A3', keyCode: 'A3' },
		{ note: 'A#3', keyCode: 'A#3' },
		{ note: 'B3', keyCode: 'B3' },
		{ note: 'C4', keyCode: 'C4' }, // Second octave
		{ note: 'C#4', keyCode: 'C#4' },
		{ note: 'D4', keyCode: 'D4' },
		{ note: 'D#4', keyCode: 'D#4' },
		{ note: 'E4', keyCode: 'E4' },
		{ note: 'F4', keyCode: 'F4' },
		{ note: 'F#4', keyCode: 'F#4' },
		{ note: 'G4', keyCode: 'G4' },
		{ note: 'G#4', keyCode: 'G#4' },
		{ note: 'A4', keyCode: 'A4' },
		{ note: 'A#4', keyCode: 'A#4' },
		{ note: 'B4', keyCode: 'B4' },
		{ note: 'C5', keyCode: 'C5' }, // Third octave
		{ note: 'C#5', keyCode: 'C#5' },
		{ note: 'D5', keyCode: 'D5' },
		{ note: 'D#5', keyCode: 'D#5' },
		{ note: 'E5', keyCode: 'E5' },
		{ note: 'F5', keyCode: 'F5' },
		{ note: 'F#5', keyCode: 'F#5' },
		{ note: 'G5', keyCode: 'G5' },
		{ note: 'G#5', keyCode: 'G#5' },
		{ note: 'A5', keyCode: 'A5' },
		{ note: 'A#5', keyCode: 'A#5' },
		{ note: 'B5', keyCode: 'B5' },
		{ note: 'C6', keyCode: 'C6' }
	];

	const keyFrequencies = {
		C3: { frequency: 130.81 }, // C3
		'C#3': { frequency: 138.59 }, // C#3/Db3
		D3: { frequency: 146.83 }, // D3
		'D#3': { frequency: 155.56 }, // D#3/Eb3
		E3: { frequency: 164.81 }, // E3
		F3: { frequency: 174.61 }, // F3
		'F#3': { frequency: 185.0 }, // F#3/Gb3
		G3: { frequency: 196.0 }, // G3
		'G#3': { frequency: 207.65 }, // G#3/Ab3
		A3: { frequency: 220.0 }, // A3
		'A#3': { frequency: 233.08 }, // A#3/Bb3
		B3: { frequency: 246.94 }, // B3
		C4: { frequency: 261.63 }, // C4
		'C#4': { frequency: 277.18 }, // C#4/Db4
		D4: { frequency: 293.66 }, // D4
		'D#4': { frequency: 311.13 }, // D#4/Eb4
		E4: { frequency: 329.63 }, // E4
		F4: { frequency: 349.23 }, // F4
		'F#4': { frequency: 369.99 }, // F#4/Gb4
		G4: { frequency: 392.0 }, // G4
		'G#4': { frequency: 415.3 }, // G#4/Ab4
		A4: { frequency: 440.0 }, // A4
		'A#4': { frequency: 466.16 }, // A#4/Bb4
		B4: { frequency: 493.88 }, // B4
		C5: { frequency: 523.25 }, // C5
		'C#5': { frequency: 554.37 }, // C#5/Db5
		D5: { frequency: 587.33 }, // D5
		'D#5': { frequency: 622.25 }, // D#5/Eb5
		E5: { frequency: 659.26 }, // E5
		F5: { frequency: 698.46 }, // F5
		'F#5': { frequency: 739.99 }, // F#5/Gb5
		G5: { frequency: 783.99 }, // G5
		'G#5': { frequency: 830.61 }, // G#5/Ab5
		A5: { frequency: 880.0 }, // A5
		'A#5': { frequency: 932.33 }, // A#5/Bb5
		B5: { frequency: 987.77 }, // B5
		C6: { frequency: 1046.5 } // C6
	};

	function playSound(event) {
		const { keyCode } = event;
		const key = keys.find((key) => key.keyCode === keyCode);
		if (key) {
			const { frequency } = keyFrequencies[key.note];
			const audio = new Audio(`sounds/${frequency}${key.note}.mp3`);
			audio.play();
		}
	}

    // Function to handle keydown event
    function handleKeyDown(event) {
    if (event.key === 'Shift') {
      // Check if it's the left shift key
      if (event.location === 1) {
        console.log("Left Shift pressed");
        // Handle left shift press
      } else if (event.location === 2) {
        console.log("Right Shift pressed");
        // Handle right shift press
      }
      shiftPressed = true;
    } else {
      const keyCode = keyMap[event.key];
      if (keyCode) {
        // Handle other keys
        console.log(`Key pressed: ${event.key}, KeyCode: ${keyCode}`);
      }
    }
  }

	window.addEventListener('keydown', handleKeyDown);
</script>

{#each keys as { note, keyCode }}
	<div class="key" on:click={() => playSound({ keyCode })}>{note}</div>
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
