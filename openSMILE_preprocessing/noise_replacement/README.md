# noise_replacement
Scripts to replace unwanted noise with reasonable ambient replacement noise.

# fftnoise

Matlab script written by Aslak Grinsted. Ported to Python by Frank Zalkow.

## fftnoise(f)

## band_limited_noise(min_freq, max_freq, samples=1024, samplerate=1)

# generate_sample
Script to find a 2.5 second clip of ambient noise and silence that clip.

## build_sample(path, original, chosen_one, mask)
Function to create a sample file in which the chosen clip of ambience is
replaced with a cloned clip of ambience.

## check_clip_len(options, duration)
Function to determine the number of clips of a specified duration.

## create_sample(in_file)
Function to iterate through [top_directory]/URSI/[subdirectory]/files structure
and perform a function on each file.

## export(audio_segment, out_path)
Function to export a pydub audio segment to a local waveform file.

## out_file_path(path, method)
Function to build an export filepath based on the original filepath and the
method being investigated.

# noise_replacement
Script to replace silenced noises in data sound files.

## analyze_and_generate(path)
Function to find ambient clips, get their amplitude and power spectrum, and]
generate an ambeint mask based on this information.

## borders_frames_to_ms(borders, rate)
Function to convert a list of 2-item lists or tuples from frames to
milliseconds.

## borders_ms_to_frames(borders, rate)
Function to convert a list of 2-item lists or tuples from milliseconds to
frames.

## build_new_soundfile(with_silence, rate, mask, borders = None)
Given a soundfile, an optional mask, and a list of time-pairs, concatenate the
segments outside of the time-pairs, replacing the time-pair marked segments
with the mask, if applicable.

## fill_in(mask, duration, rate)
Get a section of a mask of the specified duration.

## get_ambient_clips(path)
Find sections of ambient noise at least 2 seconds long.

## grow_mask(mask, size)
Function to create a clone mask from an ambient clip.

## replace_silence(original, mask, rate)
Function to create a clip in which silences are replaced by masks.

# nr_openSMILE
Script to run selected openSMILE config files on sound files with noises
replaced by various methods (see [`openSMILE_preprocessing/noise_replacement`](https://github.com/shnizzedy/SM_openSMILE/tree/master/openSMILE_preprocessing/noise_replacement "noise_replacement") for noise replacement details).

## run_openSMILE(config_file, sound_file)
Function to run the openSMILE with a specified config_file on a specified
sound file and save the results.

# Method used to determine appropriate noise masking method

## Data

Participants:
n = 42

Conditions:
n[c] = 2 × 2 = 4
{ button push, vocal response } × { stranger present, stranger not
present }

Collected data:
50 ~3" waveform files × participant × participated condition

## openSMILE: emobase.conf

To get an idea of what openSMILE was used with emobase.conf (openSMILE
configuration file for live emotion recognition base set of 988
features, 1st level functionals of low-level descriptors such as MFCC,
Pitch, LSP, ...) set of 150 or 200 waveform files (3 or 4 conditions
with 50 waveforms each) with each file lasting ~3 seconds.

## Random Trees

- [ ] *write this section*

# Removing noise
Each 0:00:03 waveform begins with a beep. To remove these unwanted beeps,
0:00:0.16 was initially clipped from the beginning of each 0:00:03 waveform
file and the files for each condition per participant were concatenated :
each participant has a maximum of 4 (n[c]) ~0:02:30 waveform files.

# Testing options

## Proof of concept

To pilot noise masking options, `M00437100_vocal_no_long_no_beeps.wav` was
selected randomly from the subset of data files that included participants
without a SM diagnosis and in a stranger-not-present condition trial. The clips
listed in the trial blocks below were analyzed by openSMILE with the 
`emobase.conf` and `ComParE_2016.conf` configuration files using the default
parameters for each.

Three blocks of comparisons were made.

### Ambient noise in trial block

`ambient_noise_silenced`: A modified version of the original file was created
in Audacity in which a 2.5 second clip of ambient noise beginning at 25.864
seconds was removed.

This clip `ambient_noise_silenced.wav` was compared against `original.wav` &
the following modifications of itself:

`ambient_noise_replaced_with_clone`: a clone mask was created by copying a 2.5
second clip (from the same file beginning at 4.713 seconds) into a new audio
track, reversing this clip and appending the reversed clip to reach 5 seconds,
then repeating this pattern to reach the full 00:02:27.24 length of
`original.wav`, clipping the end to make the durations match. The 2.5 seconds
of this clone mask beginning at 25.864 seconds was mixed in to
`ambient_noise_silenced.wav` to create the file for this condition.

`ambient_noise_clone_throughout.wav`: the aforementioned clone mask was mixed
throughout the duration of `ambient_noise_silenced.wav` to create this
condition.

`ambient_noise_replaced_with_stretch.wav`: the half-second of ambient noise
immediately preceding the silenced 2.5 seconds in `ambient_noise_silenced.wav`
was stretched to fill the silence in this condition.

`ambient_noise_replaced_with_brownian`, `ambient_noise_replaced_with_pink`,
`ambient_noise_replaced_with_white`: brownian, pink, and white noise, 
respectively, were generated by Audacity to fill the 2.5 seconds of silence in
`ambient_noise_silenced.wav` to create these conditions.

`ambient_noise_replaced_with_timeshift.wav`: the 2.5 seconds of silence in 
`ambient_noise_silenced.wav` was simply deleted to create this condition.

### Ambient noise isolated

`original_only_ambient_noise.wav`: the 2.5 seconds of ambient noise removed
from `original.wav` to create `ambient_noise_silenced.wav` was used as the
baseline for this trial block.

`only_ambient_noise_replaced_with_clone.wav`: the 2.5 seconds of clone mask
mixed into `ambient_noise_replaced_with_clone.wav` was isolated for this
condition.

`only_ambient_noise_replaced_with_stretch.wav`: the stretched 2.5 second clip
used to fill the silence in `ambient_noise_replaced_with_stretch.wav` was
isolated for this condition.

`only_ambient_noise_replaced_with_brownian.wav`: 2.5 seconds of brownian noise
was generated by Audacity for this condition.

`only_ambient_noise_replaced_with_silence.wav`: 2.5 seconds of silence was
generated by Audacity for this condition.

### Actual noise in trial block

As in the ambient noise trial block, these clips were compared against
`original.wav`.

`noise_replaced_with_silence.wav`: 2.178 seconds beginning at 00:01:51.632
which included an audible cough were silenced to create this condition.

`noise_replaced_with_clone.wav`: the corresponding 2.178 second segment of the
clone mask used in the ambient noise trial block was mixed in to the silenced
section of `noise_replaced_with_silence.wav` to create this condition. 

`noise_clone_throughout.wav`: the entire clone mask used in the ambient noise
trial block was mixed in to `noise_replaced_with_silence.wav` to create this
condition.

`noise_replaced_with_timeshift.wav`: the silenced section of
`noise_replaced_with_silence.wav` was deleted to create this condition.

### Summary statistics

Using the number of mean absolute deviations within each trial block for each
configuration file, summary measures (sum, mean, median) are calculated to
rank the closeness of each condition to the original (see [Klein, A., Andersson, 
 J., Ardekani, B. A., Ashburner, J., Avants, B., Chiang, M.-C., . . . Parsey,
 R. V. (2009). Evaluation of 14 nonlinear deformation algorithms applied to
 human brain MRI registration. *Neuroimage, 46*(3), 786–802](https://mfr.osf.io/render?url=https://osf.io/7fvme/?action=download%26mode=render "Evaluation of 14 nonlinear deformation algorithms applied to human brain MRI registration.") for an explanation of ranking by MADs).
 
[`SM_openSMILE\openSMILE_preprocessing\condition_comparison.py`](https://github.com/shnizzedy/SM_openSMILE/blob/master/openSMILE_preprocessing/condition_comparison.py "condition_comparison.py")
contains the code used to process the openSMILE output data, which are
available in [`SM_openSMILE/openSMILE_preprocessing/openSMILE_outputs/`](https://github.com/shnizzedy/SM_openSMILE/tree/master/openSMILE_preprocessing/openSMILE_outputs "openSMILE_outputs").

# Removing noise again
0:00:0.16 proved to be insufficient to remove all of the beeping noises.
The noise removal procedure mentioned above was repeated on the original
soundfiles, this time removing 0:00:0.25 from each 0:00:03 waveform prior
to concatenation.
