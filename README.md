# ZenithLite
 A custom wrap-up module of SVDEnsemble by Han Shuting https://github.com/hanshuting/SVDEnsemble .

This repository provides a small wrapper around the SVDEnsemble codebase, tailored to our project needs. In particular, the aim of this repo is to link visual stimuli to the ensembles detected by SVDEnsemble and determine whether the detected ensembles represent any subset of the visual stimuli.

QUICK RUN:

For a quick example test run, load the variables from the exampleData directory and call:

[OUT, fig] = findEnsembles(spikeMatrix, ensembleParameters, roiCoordinates, stimuliStruct, stimuliParameters);

in MATLAB.

EXPERIMENT STRUCTURE:

In this context, an experiment or session refers to a series of recordings performed within a given time window on a single animal. Each recording within a session is acquired while presenting a specific type of visual stimulus. In our experiments, visual stimuli consisted of gratings with varying contrast values: alpha ∈ {0, 5, 8, 20, 30, 50, 100}.
During a single recording, the visual stimulus starts at a specific time and stops shortly afterward. For this code, you need to know the time frame indices at which the stimulus starts and ends.
Calcium data for each ROI is normalized using ΔF/F and then converted to inferred spike data. Spike data from all recordings in the experiment are concatenated into a single spike matrix.

PARAMETER FORMAT AND EXAMPLE:

Example scenario:
Five recordings were obtained at a 30 Hz sampling rate, each lasting 10 seconds. Visual stimuli were presented between 6 and 8 seconds. Twenty ROIs were identified, and their spike activity was computed.

The spike raster (spikeMatrix) would therefore have dimensions 20 × 1500 (since each recording has 300 frames). roiCoordinates would have dimensions 20 × 2, where the first column contains x-axis coordinates and the second column contains y-axis coordinates.

stimuliStruct would be a struct of size 5 (one per recording), with at least two fields:
stimuliStruct(numberOfRec).t – a vector containing either the real time axis for that recording or simply the frame indices (for example 1:300).
stimuliStruct(numberOfRec).alpha – a scalar indicating which stimulus was presented during that recording.
stimuliParameters must specify the frame indices when the visual stimulus starts and ends, and which field from stimuliStruct should be used as the stimulus label.

Example:

stimuliParameters.stimulusFieldName = 'alpha';
stimuliParameters.stimulusStartAndEndFrames = [180, 240] %(from 6s to 8s at 30 Hz)

See the provided sample data for a realistic example of the required data format.


