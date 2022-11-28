
### Why image segmentation in medical imaging is useful ?

* It enables us to quantify the anatomy of the patients. In other words, carrying out quantitative analysis becomes possible. Then, those measurements can
  be used as features for classification and regression of diseases. Some of quantitative measurements via segmentation are given below.
  
  - Measuring the volume of ventricular cavity
  - Measuring the size of the liver

* Segmentation masks help to determine the location and extent of an organ or a certain type of tissue like white matter, gray matter or a tumor 
  for medical treatment such as radiation therapy.
  
* Creating 3D models becomes easier with segmentation masks. Then, these models can be used for simulation. For example, a model of abdominal aortic 
  aneurysm is very successful for simulating stress distributions. 

### Which information can be extracted from medical images via segmentation ?

* Size of anatomical structures
* Shape of anatomical structures
* Position of anatomical structures

### Partial Volume Effect:

Partial volume effect is, in some resources, categorized as a type of artifact observed in 3D medical imaging modalities. In volumetric images, 3D 
continuous objects such as brain or heart is represented by discrete limited amount of voxels. At that time, multiple tissues may contribute to intensity 
value of a voxel. In other words, more than one tissue correspond to same voxel, so the intensity of that voxel becomes mixed. In other words, the reason
for partial volume effect is the discretization of 2D image signal in continuous domain. This triggers partial volume effect, and thereby causing blurring 
of intensity values on tissue boundaries. Thinner slicing can be useful to alleviate this problem. 

### Intensity Inhomogeneity

Intensity inhomogeneity is the situation when intensity values tend to vary instead of being static. In this case, same tissue type can be illustrated 
with different tones of intensity values. For example, some parts of gray matter in the brain get closer to white color in the scan. This causes shading 
artifact to appear over the image, which reduces the performance of medical imaging methods that assume the intensity of a tissue class is constant over 
the range of the image.

Many image processing tasks based on MRI scans like segmentation and registration are strictly dependent on the quality of the images, because they use 
intensity values as a principal feature. These tasks are vulnerable to intensity inhomogeneity (IIH), also known as the bias field or gain field.

Intensity inhomogeneity is commonly observed in MRI scans, and in general it is caused by the presence of non-uniformity in the radio-frequency (RF) coil. 
Histogram equalization is one of the methods that can be used to solve this problem; however, it also tend to increase the noise in MRI scans. 7-Tesla and 
9-Tesla MRIs generate higher resolutional images, but intensity inhomogeneity comes up as a tradeoff. 

### Image Geometry:

Image geometry is very important to segmentation and registration. In segmentation, segmented voxels of every tissue type is multiplied by the size of 
one voxel to compute entire volume. At this point, the voxels can be of isotropic or anisotropic. 

- **Isotropic voxel:** voxel of same length in every dimension
- **Anisotropic voxel:** voxel of different length in its dimensions

One of the main reasons why anisotropic voxels are used is awfulness of patients. In purpose, longer voxels through the depth axis are used to reduce 
scanning time. This is called "Manhattan voxels". 

### Limited Contrast:

Limited contrast is one of the problems that can directly affect the performance of medical imaging segmentation techniques. Different tissues might 
have similar physical properties, so they can be illustrated with similar intensity values in imaging modalities. In this case, differentiating adjacent 
but different tissue types becomes harder. Purely intensity-based segmentation algorithms such as region growing are prone to leak into adjacent tissue. 

### Imaging Artifacts:

Artifacts in medical images can be described as everything that makes entire image or some part of it deviate from what is present in actual anatomy, and
they can severely degrade the performance of segmentation algorithms. In general, there are two main sources of artifacts in medical images.

1. Patients' motion during imaging (This motion can cause blurring inside the images)
2. Implants and clothing (They can distort the image)

There are also other factors that can cause the artifacts in medical imaging, but these are the most common two ones. In general, noise and partial volume 
effect are not included in the scope of artifacts. Especially, partial volume effect is a commonly observed problem due to the discretization of continuous 2D imaging signals. 

### Ground-Truth Segmentation Masks in Medical Imaging:

To evaluate the performance of segmentation algorithms, we need to have ground-truth masks to be compared with the predictions of those algorithms. At that
point, experienced clinicians and experts are asked to segment the images manually, and their manual segmentation masks are considered as reference for it. However, this process have 3 important shortcomings:

1. Manual annotation is very tedious and time-consuming, since medical images are 3D volumetric data of many 2D slices. 
2. It is not easy to get accurate segmentation masks; the experts may make a mistake during manual annotation. At this point, two different sub-problems occur.

- Intra-observer Variability: The manual segmentation made by a clinical expert can vary depending on his/her conditions. (Disagreement between same expert)
- Inter-observer Variability: The manual segmentation made by different clinical experts can be different from one another. (Disagreement between different experts)

To solve this problem, two main approaches are recommended. If manual segmentation of medical images is carried out by many different experts, we can take average of their variabilities and quantify the uncertainities between those experts. In that way, variability problem is solved and we can end up with the most accurate segmentation masks. To reduce the time-complexity problem, a simple segmentation algorithm can be used. It segments the organs and tissues; the clinicians only correct the mistakes made by the algorithm. 


### Confusion Matrix:


|                 | `Cond Positive` | `Cond Negative` |
| ---             |     ---         |      ---        |
| `Pred Positive` |  True Positive  |  False Positive |
| `Pred Negative` | False Negative  |  True Negative  |

* TP: Correctly Diagnosed Patients (Hits)
* TN: Correctly Diagnosed Healthy Subjects (Correct Rejections)
* FP: False Alarm (type-1 error, causing wrong treatment to be applied to healthy subject)
* FN: Missing a disease (type-2 error, causing the delay of patient treatment)

Specifically, brain atrophy and breast cancer have a lot of false positive cases. 

### Evaluation Metrics:

* **Accuracy:** $\frac{TP + TN}{P + N}$ (Trueness, How many predictions made by the model are correct)
* **Precision:** $\frac{TP}{TP + FP}$ (Positive Predictive Value, How many detections or segmented regions by the model are correct)
* **Sensitivity:** $\frac{TP}{TP + FN}$ (True Positive Rate, Hit Rate, How many objects exist in the image and how many of them are correctly detected by the model)
* **Specificity:** $\frac{TN}{TN + FN}$ (True Negative Rate, What is total background region in ground-truth and how much of it is correctly segmented by the model)


For the segmentation of anatomical structures in human body by deep learning models, the most-commonly used quantitative performance measurements for evaluating segmentation performance of the model are

1) Classical Confusion Matrix Metrics: Precision and Recall
2) Overlap-based Measurements: Dice Score and IOU (Jacard Index)
3) Hausdorff and Mahalanobis Distance

### Why U-Net is very good architecture in segmentation of medical images ?

* The spatial features and low level details of image context would be preserved and transfered to decoder part by skip connections so that they can be used for creating segmentation masks. 

* Skip connections enable the network to have a good gradient flow from decoder to encoder during the backpropagation. 

### Why is vessel and coronary segmentation very important ?

Retinal vessel segmentation provides necessary pieces of information for us to have correct clinical diagnosis of ocular diseases, such as macular degeneration, diabetic retinopathy, and glaucoma. Likewise, some changes on coronary arteries can be identified by coronary segmentation, which may be possible indications of hypertension, myocardial infarction, and coronary atherosclerotic disease.

## Classical Image Segmentation Algorithms:

### 1. Thresholding:

Thresholding is the simplest algorithm used to segment the objects from the background. It creates a binary image from gray-scale image. Most of the thresholding algorithms are intensity histogram-based. 

We just create intensity the histogram of pixels and identify the peaks on that histogram plot. Peak regions refer to the most dominant areas on the image. When we choose a threshold value, we would ignores all the pixels in the image whose intensity values are lower than that threshold, and the remaining pixels are regarded as foreground. In that way, segmentation would be performed. While doing thresholding, it is also possible to determine lower and upper thresholds together to particularly select the area between them. 

Advantages:

- It is very simple algorithm.
- It works quite fast.

Disadvantages:

- It can be easily affected by the noise and artifacts. If the images have so many artifacts, thresholding method can fail. The regions in the image must be homogeneous and distinct. 

- It is quite difficult to find consistent thresholds across images. 

### 2. Region Growing:

Region growing is a recursive segmentation algorithm. First of all, it takes a starting point from the user, which is a pixel coordinate in the image, and mark its neighboring pixels with similar intensity value. Then, its calls itself for the neighboring pixels of all marked pixels. In that way, it grows the region and the pixels with similar intensities would be segmented. At this point, whether the pixels have similar intensity values or not actually depend on pre-defined intensity threshold and starting seed point.

Advantages:

- It is relatively fast approach.
- Since it looks at the neighbors, it gives us one connected region starting from seed point. In that way, it enables us to track particular continuous regions like white matter in the brain or particular vessel in retinal image. However, tracking same, but separated regions like CSF in the brain requires more than one seed point. 

Disadvantages:

- The regions in the image needs to be homogeneous. Artifacts and noise can easily affect the performance of region growing algorithm. 
- It depends on the user (semi-automatic algorithm), since seed point is given to the algorithm by the user.

### 3. Graph Cut:

Graph cut is a segmentation algorithm based on max-flow min-cut theorem. It is a semi-automatic algorithm; it expects the use to give scribbles (seed brushes) as reference input. These input values are used to define which regions will be kept and which regions need to be removed (foreground and background) in the image. 

Graph cut algorithm formulates a grid graph on image pixels, and tries to separate this graph into two or more number of disjoint sub-graphs. While doing that, it follows max-flow min-cut theorem. The boundaries between tissues (the edges) are the regions in which the flow from source to sink through the graph is maximized. 

Not only foregorund background binary segmentation but also multiple organ segmentation is possible with graph cut algorithm. 

Advantages:

- It is really fast and also accurate algorithm.
- It is not direct machine learning approach, but it contains markov random process. 
- It is reasonably efficient and interactive algorithm.

Disadvantages:

- It is a semi-atuomatic algorithm; unfortunately it depends on the user input.
- It is difficult to choose its tuning parameters correctly. 


