# Why use video?
Video recording allows us to follow the test operations after the end of the run, analysis and understanding of faults during the test, by this it is possible to understand if there is a bug in the software being tested or a bug in the test itself.
Although the recording brings us information visually, we prefer to use trace because it is easier to identify elements in trace, it is easier to analyze the test itself and of course it weighs much less than video

# How to use
So, to use video recordings like we want in Trace, we have two options: we can either use the config file or run the test. Using the config file is better because we can choose how to record the video based on these parameters:

- `'off'`: Don't record video.
- `'on'`: Record video for every test.
- `'retain-on-failure'`: Record video for every test, but delete the videos from successful test runs.
- `'on-first-retry'`: Record video only when retrying a test for the first time.