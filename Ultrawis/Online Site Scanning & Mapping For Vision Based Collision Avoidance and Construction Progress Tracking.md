### Outline
1. Data Collection Module
2. Automated creation of jobsite 3D representation.
3. Neighbor crane position detection
4. Lifted cargo dimension, position, orientation detection
5. Optimal load and unload route calculation
6. System components adjustments - camera units, sensors.
7. 

### Intro
Our system introduces a novel approach to jobsite mapping by leveraging our existing crane ADAS (Advanced Driver Assistance System) and normal crane operations. 
Our offered solution will utilize existing sensors and cameras to transform collected data into a dynamically updated 3D representation of the jobsite. All this is to be preformed automatically, in a background process, producing the 3D representation as a natural byproduct of existing daily workflows.
### Goal
The primary goals of this feature is to generate a self updating 3D representation of the jobsite to be used in a first of its kind collision avoidance system and jobsite tracking capability.
1. Accurate, adaptive collision avoidance system. 
   The system will integrate the data in the 3D representation in our collision avoidance system, to avoid colliding with static structures within the jobsite.  
2. Provide continuous construction progress tracking capability.
    By maintaining up-to-date 3D representation of the jobsite, the feature will enable site managers and engineers to monitor the construction progress, detect errors and inefficiencies and address issues as they arise.
3. Assist in route planning for cargo lifts and unloads.
### Functional Innovation & Advantages Over Existing Competition

Our solution aims to produce the first ever computer vision based collision avoidance system for construction cranes. The system will eliminate the reliance on manual configuration and will be the first system to automatically track jobsite structural changes and incorporate them into the collision avoidance model. 

- **Manual vs Autonomous Collision Avoidance system**
  Existing collision avoidance systems require laborious manual configuration of the jobsite and its surrounding. This tends to be less accurate than desired and prone to human error. It relies heavily on the competency of the human responsible for the system configuration. Moreover, manual configuration tends to be fragile, as the jobsite is continuously changing. 
  Our system will be the first to integrate 3D site mapping data into a collision avoidance system, providing an autonomous system that updates itself independently.

- **Continuous Monitoring, Seamless Integration with Crane Operations**
  Traditional site scanning and mapping are usually performed as a separate survey process, requiring dedicated equipment, dedicated time, and specialized service acquisition. 
  Usually, site scans are not performed at a high frequency that is required to keep track of daily changes.
  Our solution runs in the background while cranes are in operation, providing a steady stream of site data. This continuous scanning is more effective than periodic manual scans, offering a comprehensive and up-to-date view of the construction site.
  
- **Reduced Costs and Time**
   By repurposing our ADAS system for site scanning, construction companies can avoid the expense of dedicated scanning devices, and the effort involved in performing separate site surveys. This contributes to lower overall project costs and reduced equipment clutter on-site.
   
- **Seamless Integration with Crane Operations**
   Our system integrates with existing crane controls and sensors, ensuring that site scanning occurs without interfering with crane operations. This seamless integration enhances the overall efficiency of construction projects.
    

Overall, our automated site scanning solution presents a more efficient, cost-effective, and integrated approach to construction site monitoring, setting it apart from traditional solutions that require additional equipment and dedicated scanning time. By leveraging the inherent scanning capabilities of cranes, we provide construction companies with a robust and innovative tool for improving site management and safety.

### Technological Innovation


### Task Breakdown
1. **Development of data collection module for later offline processing**.
   - Each crane should have a data collection module that collects imagery and relevant sensor information based on crane state, time of day etc.
   - **Metadata Annotation** - imagery should be annotated with additional metadata such as
	   - Time collected
	   - World position and orientation
	   - Crane Sensor data such as load, crane positioning
	   - Camera extrinsics and intrinsics
   - **Cloud Data Management** - A cloud database for collected data should be managed, allowing easy retrieval of collected data in order to feed 3D structural mapping algorithms.
2. **Development of calibration procedures for crane cameras and sensors**.
	 - **Camera Calibration Requirements**: 3D reconstruction requires precise calibration of cameras and sensors. This involves determining camera parameters and spatial alignment for accurate modeling.
	- **Calibration Equipment and Techniques**: Some calibration procedures might require specialized equipment, such as calibration boards or dedicated devices. Calibration should account for variations in lighting and crane movement to maintain accuracy.
	- **Continuous Calibration Monitoring**: Procedures to regularly check and adjust calibration to maintain precision over time.
4. Algorithm for constructing a 3D jobsite representation.
   A unique algorithm that analyses the collected data, uses advanced structure from motion techniques, to produce both an initial 3D model, and update it when new data is collected.
   
   
   This task will incorporate both state of the art 
    Adjust, innovate, and fine-tune selected frameworks to meet the unique needs of the site scanner. Implement custom algorithms and processes to ensure reliable 3D reconstruction.
   This can be further break down into the following sub tasks:
	1. Implementation of 2D "aerial image stitcher" of site to provide a high resolution site tracker from upper view.
	2. Implementation of full scale 3D reconstruction of site.
	3. Timelapse capability - allowing site managers to track site progress along a timeline.
	4. Anti Collision Integration - integration of reconstructed model with anti collision system to allow.
### Technological Challenges
- **Image Quality and Coverage**: Achieving high-quality image data with crane-mounted cameras can be challenging due to limited crane movement, non-ideal positioning for site mapping. Ensuring adequate coverage of the entire construction site requires optimal placement and orientation of cameras.
- **Accurate, Robust Calibration**: All cranes sensors and cameras must be properly calibrated, and account for changes in crane configuration and positioning.
- **Algorithmic Challenges**: Creating a 3D representation of the scanned area from 2D camera data is a complex problem. The system must accurately derive depth and spatial information from multiple perspectives, requiring advanced computer vision techniques and calibration methods. Changes in lighting, crane movement, and varying environmental conditions add to the complexity.
- **Data Processing and Analysis**: Scanning and analyzing data in real-time demands powerful processing capabilities. The system must be able to process images and other sensor data to generate accurate site maps without interfering with crane operations.
- **Data Synchronization**: Ensuring consistent alignment of data from multiple cranes, which requires precise synchronization of spatial and temporal information.



### Human Resources

| Milestone / Task                 | Estimated Manhours |
| -------------------------------- | ------------------ |
| Data Collection Module           | 0.5y               |
| Calibration Procedures           | 0.5y               |
| Research of existing techniques  | 0.33y              |
| Proprietary Solution             | 2y-3y              |
| Site Integration and experiments | 0.5y               |
| Product Characterization         | 0.5y               |
| Total                            | ~5y                |
