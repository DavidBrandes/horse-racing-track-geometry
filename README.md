# Horse Racing Track Geometry

A geometry-focused research prototype for transforming horse-racing GPS traces
into track-relative coordinates. It was developed from the tracking data released
for Kaggle's [Big Data Derby 2022](https://www.kaggle.com/competitions/big-data-derby-2022/overview).

Instead of describing a horse only by latitude and longitude, the model derives
features that are easier to use in analysis:

- distance remaining to the finish line;
- lateral offset from the inside rail; and
- local track curvature.

The implementation fits straights and turns to sampled rail coordinates and
supports vectorized evaluation of complete race trajectories, including run-in
sections.

## Repository layout

- [`horse_racing/track`](horse_racing/track) — track construction, evaluation,
  and visualization
- [`horse_racing/utils`](horse_racing/utils) — geographic conversion, geometry,
  and least-squares fitting
- [`notebooks`](notebooks) — a rendered walkthrough of the transformation
- [`track_data/AQU`](track_data/AQU) — sampled geometry for Aqueduct Racetrack
- [`plot_track.py`](plot_track.py) and [`assess_tracks.py`](assess_tracks.py) —
  exploratory scripts used with the original Kaggle CSV files

## Quick example

Install the small scientific-Python dependency set:

```bash
python -m pip install numpy scipy pandas matplotlib
```

Then load the included track definition and transform an array of
`(latitude, longitude)` samples:

```python
from horse_racing.track.track import RaceTrack

track = RaceTrack.from_directory("track_data/AQU")
distance, offset, curvature = track(
    coordinates,
    track_id="D",
    run_in_id="D",
)
```

See the rendered [track-transformation notebook](notebooks/transforming_the_track.ipynb)
for the geometric motivation and visual results.

## Data and project status

The sampled track geometry is included, but the competition CSV files are not;
download them from Kaggle and place them under `csv/` to use the exploratory
scripts. This repository is a portfolio snapshot of the transformation approach,
not a maintained race-prediction product or betting system.

## License

MIT — see [`LICENSE`](LICENSE).
