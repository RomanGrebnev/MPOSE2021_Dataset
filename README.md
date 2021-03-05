# MPOSE2021 Dataset

This repository contains the MPOSE2021 Dataset for short-time pose-based Human Action Recognition (HAR). 

MPOSE2021 is developed as an evolution of the MPOSE Dataset [1-3]. It is made by human pose data detected by OpenPose [4] on popular datasets for HAR, i.e. Weizmann [5], i3DPost [6], IXMAS [7], and KTH [8] alongside original video datasets, i.e. ISLD and ISLD-Additional-Sequences [1]. Since these datasets had heterogenous action labels, each dataset labels were remapped to a common and homogeneous list of actions.

This repository contains pose data in a python-friendly format. Moreover, it also contains the scripts to generate MPOSE2021 dataset (RGB data) starting from the original RGB sequences belonging to the above-mentioned dataset. For licence-related reasons, the user must download RGB data from the original sources, as explanined in the manual.

## Requirements
The following requirements are needed to generate RGB data for MPOSE2021 (tested on Ubuntu 20.04).
* ?? free disk space;
* Python 3.8;

## Generate RGB data
1. Clone the repository.

2. Create virtual environment (optional, but recommended).
    * venv...
    * source venv/bin/activate

3. Check and set top variables in "scripts/init_vars.py":
    * "dataset_path": where you want the dataset to be exported
    * "archives_path": where you want to save the former dataset archives (requires ??? free space)
    * "temporary_path": where temporary files will be stored (requires ??? free space)
    * "max_frame_length": maximum frame length of each MPOSE2021 sequence (default 30, don't chance for reproducibility)
    * "min_frame_length": minimum frame length for a sequence of poses to be accepted (default 20, don't chance for reproducibility)

4. Run variables initialization
    * `python init_vars.py`

5. Download RGB archives from the following third-party repositories:
    * [IXMAS Dataset](https://www.epfl.ch/labs/cvlab/data/data-ixmas10).
        * Download "original IXMAS ROIs" archive.
        * Save the archive into "arhives_path"/ixmas/.
    * [Weizmann Dataset](http://www.wisdom.weizmann.ac.il/~vision/SpaceTimeActions.html).
        * Download actions: Walk, Run, Jump, Bend, One-hand wave, Two-hands wave, Jump in place.
        * Save the archive into "arhives_path"/weizmann/.
    * [i3DPost Dataset](http://kahlan.eps.surrey.ac.uk/i3dpost_action/) (subject to password request!).
        * Download all archives related to actions: Walk, Run, Jump, Bend, Hand-wave, Jump in place.
        * Save the archive into "arhives_path"/i3DPost/.
    * [KTH Dataset](https://www.csc.kth.se/cvap/actions/).
        * Download archives "walking.zip", "jogging.zip", "running.zip", "boxing.zip", "handwaving.zip", "handclapping.zip".
        * Save the archive into "arhives_path"/kth/.
    * [ISLD Dataset]()
        * Download ???.
        * Save the archive into "arhives_path"/isld/.
    * [ISLD-Additional-Sequences Dataset]()
        * Download ???.
        * Save the archive into "arhives_path"/isldas/.

6. Install python requirements:
    * `pip install -r requirements.txt`

7. Extract archives:
    * `python extract_formers.py`
  
8. Create RGB data:
    * `python create_video.py`
    * RGB data for MPOSE2021 are located in "dataset_path"/video
    
9. Check integrity of RGB data (to make sure that the json files in "archives_path"/json are compatible):
    * `python check_integrity.py`

## Generate POSE data
1. Perform steps 1., 2., 3., and 4. from "Generate RGB data".

2. Download json data:

3. Extract json data:
    * `python extract_json.py`
    
4. Generate POSE data:
    * `python create_pose.py`

# References
[1] F. Angelini, Z. Fu, Y. Long, L. Shao and S. M. Naqvi, "2D Pose-based Real-time Human Action Recognition with Occlusion-handling," in IEEE Transactions on Multimedia. URL: http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8853267&isnumber=4456689

[2] F. Angelini, J. Yan and S. M. Naqvi, "Privacy-preserving Online Human Behaviour Anomaly Detection Based on Body Movements and Objects Positions," ICASSP 2019 - 2019 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP), Brighton, United Kingdom, 2019, pp. 8444-8448. URL: http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8683026&isnumber=8682151

[3] F. Angelini and S. M. Naqvi, "Joint RGB-Pose Based Human Action Recognition for Anomaly Detection Applications," 2019 22th International Conference on Information Fusion (FUSION), Ottawa, ON, Canada, 2019, pp. 1-7. URL: http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9011277&isnumber=9011156

[4] Cao, Zhe, et al. "OpenPose: realtime multi-person 2D pose estimation using Part Affinity Fields." IEEE transactions on pattern analysis and machine intelligence 43.1 (2019): 172-186.

[5] Gorelick, Lena, et al. "Actions as space-time shapes." IEEE transactions on pattern analysis and machine intelligence 29.12 (2007): 2247-2253.

[6] Starck, Jonathan, and Adrian Hilton. "Surface capture for performance-based animation." IEEE computer graphics and applications 27.3 (2007): 21-31.

[7] Weinland, Daniel, Mustafa Özuysal, and Pascal Fua. "Making action recognition robust to occlusions and viewpoint changes." European Conference on Computer Vision. Springer, Berlin, Heidelberg, 2010.

[8] Schuldt, Christian, Ivan Laptev, and Barbara Caputo. "Recognizing human actions: a local SVM approach." Proceedings of the 17th International Conference on Pattern Recognition, 2004. ICPR 2004.. Vol. 3. IEEE, 2004.
