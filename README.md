# layback_modeling
A Keras model to estimate underwater camera location

## Rationale
A LayBack model for georeferencing underwater imagery from a towed camera system

While Multi-Beam Echo Sounder (MBES) data can provide a magnificent understanding of the seafloor, e.g., in terms of seabed geomorphology and substrate characteristics, it is only by combining MBES data with direct underwater observations that scientists can directly relate seabed features to habitat types, species diversity, and their distribution. Because this link is spatially based, the georeferencing accuracy of the ground truth data is paramount.

The problem is more significant as the depth increases and can be addressed by adopting accurate underwater positioning systems (e.g., ultra-short baseline, USBL). Still, sometimes this is not applicable due to time, economic, and operational constraints.

We set up this imagery georeferencing problem as a multivariate regression and tackled it using Deep Neural Networks. The model consists of two parts; The first part estimates the planar distance of a towed camera from the vessel location. The second part calculates the camera position based on the vessel's position, direction, and estimated distance. 

The model uses vessel and camera Inertial Measurement Unit (IMU) data as predictor variables and predicts the vessel-camera planar distance (response variable). As ground truth, we used navigation data from a survey where Ultra-short baseline acoustic positioning (USBL) had been used in the same towed-camera system.

Before training the model, an extensive data cleaning and pre-processing operation are conducted, including filtering unwanted conditions and performing conversion of the ‘dx’ and ‘dy’ offset from the USBL data into a 'distance value.' Upon training, the model can estimate the vessel-camera distance, which is then used in a distance-bearing Vincenty formula to derive the final, corrected camera position.

The adjusted camera position is made available over the network, allowing one to 'plug in' the estimated values into other software, e.g., during the acquisition of Multi-Beam echosounder  (MBES) data for real-time visualization of the towed camera position during a survey. In addition to increased navigation safety, the image quality is also improved as this setup facilitates more intelligent navigation of the camera over the seafloor, for example, by enabling it to maintain a constant altitude.

