## SPS-Stereo: Slanted Plane Smoothing Stereo

SPS-Stereo is a dense stereo method employing a slanted plane model. It jointly estimates a superpixel segmentation, boundry labels (such as occlusion boundaries), and a dense disparity map from a pair of stereo images. It only works on a pair of stereo images whose epipolar lines are aligned vertically. SPS-Stereo then tries to estimate a horizontal disparity for each pixel location in the left image.

**Citation**  

    @inproceedings{Yamaguchi14,
    author = {Koichiro Yamaguchi and David McAllester and Raquel Urtasun},
    title = {Efficient Joint Segmentation, Occlusion Labeling, Stereo and Flow Estimation},
    booktitle = {ECCV},
    year = {2014}
    }


### Building SPS-Stereo

1. Prerequisites
    * opencv 3.4.5
2. Building
    1. type 'mkdir build && cd build/'
    2. type 'cmake ..'
    3. type 'make'


### Usage
    ./spsstereo left_image right_image output_dir


**Outputs**  

* `{left_image_basename}_disparity.png`  
Disparity image (PNG 16bit grayscale format)  
(Disparity value) = (Pixel value - 0.5)/256.0

* `{left_image_basename}_segment.png`  
Segmentation image (PNG 16bit grayscale format)  
(Segment ID) = (Pixel value)

* `{left_image_basename}_plane.txt`  
Estimated disparity planes  
the number of lines = the number of segments  
Each line includes parameters of disparity plane of a segment: `(A_i, B_i, C_i)`

* `{left_image_basename}_label.txt`  
Boundary labeling result  
the number of lines = the number of boundaries  
Each line includes three entries: `SegmentID1 SegmentID2 boundary_label`  
`boundary_label`: 0 (Occlusion, SegmentID1 is front), 1 (Occlusion, SegmentID2 is front), 2 (Hinge), 3 (Coplanar)

* `{left_image_basename}_boundary.png`  
Visualization of segmentation result  
Boundary color means a type of relationship between neighboring segments: Red/Blue-Occluion (Red side is front), Green-Hinge, Gray- Coplaner


### License
SPS-Stereo is licensed under the GNU General Public License Version 3 (GPLv3), see [http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html).