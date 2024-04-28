Our system introduces a novel approach to construction site scanning by leveraging the existing cameras installed on cranes. Unlike traditional site scanning solutions that require separate equipment and dedicated time, our platform transforms crane cameras into an automated site scanning tool, running in the background without disrupting daily workflows.
### Goal

The primary goal of this feature is to increase efficiency and reduce the costs associated with site scanning. By utilizing the cameras already in place, we eliminate the need for additional scanning equipment and minimize the overhead involved in separate site surveys. This not only reduces setup costs but also ensures that scanning occurs as a natural byproduct of crane operations.
### Innovation

Our system can capture real-time data throughout the workday, allowing for continuous site monitoring. This provides a dynamic and up-to-date view of the construction site, enabling site managers to detect and address issues as they arise. It also facilitates easier compliance with safety regulations and quality control standards.
Additionally, we plan to integrate this solution with our existing inter-crane anti collision system. Making it the first anti collision system that does not require manual maintenance and configuration.
### Advantages Over Existing Competition

Compared to traditional site scanning solutions, which often require separate hardware and manual intervention, our system offers several key advantages:

- **Reduced Equipment Costs**: By repurposing crane cameras for site scanning, construction companies can avoid the expense of dedicated scanning devices. This contributes to lower overall project costs and reduced equipment clutter on-site.
    
- **Continuous Scanning**: The system runs in the background while cranes are in operation, providing a steady stream of site data. This continuous scanning is more effective than periodic manual scans, offering a comprehensive and up-to-date view of the construction site.
    
- **Seamless Integration with Crane Operations**: Our system integrates with existing crane controls and sensors, ensuring that site scanning occurs without interfering with crane operations. This seamless integration enhances the overall efficiency of construction projects.
    
Overall, our automated site scanning solution presents a more efficient, cost-effective, and integrated approach to construction site monitoring, setting it apart from traditional solutions that require additional equipment and dedicated scanning time. By leveraging the inherent scanning capabilities of cranes, we provide construction companies with a robust and innovative tool for improving site management and safety.

### Technological Challenges
- **Image Quality and Coverage**: Achieving high-quality image data with crane-mounted cameras can be challenging due to limited crane movement, non-ideal positioning for site mapping. Ensuring adequate coverage of the entire construction site requires optimal placement and orientation of cameras.
- **Accurate, Robust Calibration**: All cranes sensors and cameras must be properly calibrated, and account for changes in crane configuration and positioning.
- **Algorithmic Challenges**: Creating a 3D representation of the scanned area from 2D camera data is a complex problem. The system must accurately derive depth and spatial information from multiple perspectives, requiring advanced computer vision techniques and calibration methods. Changes in lighting, crane movement, and varying environmental conditions add to the complexity.
- **Data Processing and Analysis**: Scanning and analyzing data in real-time demands powerful processing capabilities. The system must be able to process images and other sensor data to generate accurate site maps without interfering with crane operations.
- **Data Synchronization**: Ensuring consistent alignment of data from multiple cranes, which requires precise synchronization of spatial and temporal information.

### Task Breakdown
1. **Development of data collection module for later offline processing**.
   - Each crane should have a data collection module that collects imagery and relevant sensor information based on crane state, time of day etc.
   - **Metadata Annotation** - imagery should be annotated with additional metadata such as
	   - Time collected
	   - World position and orientation
	   -  Crane Sensor data such as load, crane positioning
	   - Camera extrinsics and intrinsics
   - **Cloud Data Management** - A cloud database for collected data should be managed, allowing easy retrieval of collected data in order to feed 3D structural mapping algorithms.
2. **Development of robust calibration procedures for crane cameras and sensors**.
	 - **Camera Calibration Requirements**: 3D reconstruction requires precise calibration of cameras and sensors. This involves determining camera parameters and spatial alignment for accurate modeling.
	- **Calibration Equipment and Techniques**: Some calibration procedures might require specialized equipment, such as calibration boards or dedicated devices. Calibration should account for variations in lighting and crane movement to maintain accuracy.
	- **Continuous Calibration Monitoring**: Procedures to regularly check and adjust calibration to maintain precision over time.
3. Research of existing frameworks, techniques and solutions for implementing multi view 3D reconstruction.
   Examples include [OpenMVG](https://github.com/openMVG/openMVG),, [OpenMVS](https://github.com/cdcseacave/openMVS), [ColMap](https://github.com/colmap/colmap) and others.
4. **Proprietary Solution Development**: Adjust, innovate, and fine-tune selected frameworks to meet the unique needs of the site scanner. Implement custom algorithms and processes to ensure reliable 3D reconstruction.
   This can be further break down into the following sub tasks:
	1. Implementation of 2D "aerial image stitcher" of site to provide a high resolution site tracker from upper view.
	2. Implementation of full scale 3D reconstruction of site.
	3. Timelapse capability - allowing site managers to track site progress along a timeline.
	4. Anti Collision Integration - integration of reconstructed model with anti collision system to allow.

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
