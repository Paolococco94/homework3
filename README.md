# HOMEWORK 3
AA 2017/2018<br>
University of Verona (Italy)

# AUTORI
  Cocco Paolo 
  Meneghetti Simone 


![immagine1]()

#DESCRIZIONE HOMEWORK
Homework 3 è composto da 4 parti

	Parte 1: installazione di ORB_SLAM2
	Parte 2: esecuzione di ORB_SLAM2 su una rosbag registrata con un drone volante
		Il link al file.bag: http://robotics.ethz.ch/~asl-datasets/ijrr_euroc_mav_dataset/vicon_room1/V1_01_easy/V1_01_easy.bag
	Parte 3: creazione di una point cloud 
	Parte 4: clustering dei punti contenuti nella point cloud generata al punto 3


#PARTE 1
	
	Si installi il software ORB_SLAM2 contenuto nel repository
        Il link: https://github.com/raulmur/ORB_SLAM2
        con compilazione ROS

#PARTE 2

	Processare la rosbag V1_01_easy.bag i seguenti comandi utilizzando tre terminali 

	$ roscore
	$ rosrun ORB_SLAM2 Stereo Vocabulary/ORBvoc.txt Examples/Stereo/EuRoC.yaml true
	$ rosbag play --pause V1_01_easy.bag /cam0/image_raw:=/camera/left/image_raw /cam1/image_raw:=/camera/right/image_raw
	
	Ecco il risultato:
	![immagine2]()
	![immagine3]()
	![immagine4]()

#PARTE 3
	
	Per la realizzazione della point cloud, sono stati modificati 3 file contenuti in ORB_SLAM2 (System.cc - System.h - ros_stereo.cc)
	E' stata implementata la funzione  " void SavePointCloud(const string &file); " la quale:
	- estrae tutti i punti dalla mappa
	- crea l'header del file PCD
	- scrive sul file i punti estratti
	
	Link per visionare la funzione: https://medium.com/@j.zijlmans/orb-slam-2052515bd84c
	Viene creato alla fine: SavePointMap_PCD.pcd

	NOTA: Per evitare che alla fine della creazione della mappa alcuni dispositivi (tra i quali il pc su cui è stato sviluppato il progetto HP 650) innestare un ciclo nell'eseguibile:

    while( ros::ok() ){
        ros::spin();
    }

	Ecco il risultato:
	![immagine5]()

#PARTE 4
	
	La clusterizzazione dei punti della point cloud generata è effettuata tramite il clustering.cpp
	Settando i valori 
	cluster_extr.setClusterTolerance(0.2); 
	cluster_extr.setMinClusterSize(50);
	dove
	0.2 rappresentano i centimetri reali (20)	
	50 il minimo numero di punti 


	NOTA:    Dato che nel file_pcd ci sono pochi punti (mappa sparsa) si potrebbero diminuire i valori delle funzioni "voxel"
                 o eliminare direttamente queste funzioni direttamente dal file di clustering
	  

	Ecco risultato finale:
	![immagine6]()




