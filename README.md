# Dragnet

Dragnet is OCR tool for Cyrillic characters using a convolutional neural network. The neural network component is powered by TensorFlow. Dragnet was produced for the Artificial Intelligence class at Reykjavik University in 2017. If you are a student in this class, we highly suggest you refrain from viewing the contents of this repository until you have handed your project in.

# Requirements

## Python Packages

    tensorflow
    pillow

## GNU/Linux Utilities

    imagemagick


# Training Dragnet

To train dragnet one must first produce the training set data.

    ./generate_training_set_images ./training_set_generator/fonts [training_images_dir]

The first argument is the location of the fonts to be used, and the second argument the directory to store the resulting images. Once the images are created, it is time to create the corresponding matrices and labels for them.

	./generate_training_set_matrices_labels.py [training_images_dir] [matrices_file] [labels_file]

The first argument is the directory where the training images had been stored, the second argument is the location of a text file to store the corresponding matrices, and the third argument a text file to store the corresponding labels. At this point it is usually good to split the generated data into training data and testing data. At the very least, Dragnet will assume the following files to be present:

    ./training_set_data/matrices_train.txt
    ./training_set_data/matrices_test.txt
    ./training_set_data/labels_train.txt
    ./training_set_data/labels_test.txt

They can be generated by running:

    ./split_training_set_data.sh [size]

Where [size] is the number of records in `./training_set_data/matrices.txt` to be used for training. The rest will be used for testing. Now the network is ready to be trained.

	./dragnet_nn_train.py --overwrite_brain

This can take some time depending on what sort of machine you are using. On a standard laptop, this is likely 1-2 hours. The argument tells the script to overwrite the contents of the previous "brain", that is, overwrite the previous configuration of the neural network. The brain is stored in the `DRAGNET_NN_BRAIN_LOCATION` variable located in `dragnet_nn/dragnet_nn.py`.

# Parsing Images

To start to parse images, simply place them in a directory and then run:

    ./generate_documents_from_images.sh [source_imgs_dir] [matrices_lables_output_dir] [final_documents_dir]

The first argument is the directory where the images to be parsed are. The second argument an intermediate location to store data while Dragnet processes it. The third argument is where the resulting text files will be placed.


# Contributors

At one point the history of the project was removed. For this reason it is especially important to recognize the contributors to this project. They are:

* James Robb [https://github.com/jamesrobb](https://github.com/jamesrobb)
* Sigurður Helgson [https://github.com/sigurdurhelga](https://github.com/sigurdurhelga)
* Sævar Valdimarsson [https://github.com/sabbisun](https://github.com/sabbisun)