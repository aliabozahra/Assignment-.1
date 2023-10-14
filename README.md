# Assignment-.1
//part 1 filter 1, 2, 3 
#include <iostream>
#include <fstream>
#include <cstring>
#include <cmath>
#include "bmplib.cpp"
///////////////////////////////////////////////// note /////////////////////////////////////////////// ////////////
// rotatw 270 w darken and ligho not done
////////////////////////////////////////////////////////////////////////////////////////////////////  //////////
unsigned char image[SIZE][SIZE];
unsigned char image2[SIZE][SIZE];

void loadImage ();
void saveImage ();
void doSomethingForImage ();
void blackandwhite();
void merge();

// sfsfssfs
//ad,las,l
//CAMERA ONLLY image[i][j]=image[i][(SIZE-1)-j];

void darkenandlight(){
    cout<<"Do you want to (d)arken or (l)ighten? \n";

    char s;cin>>s;
    if (s=='d') {
        for (int i = 0; i < SIZE; ++i) {
            for (int j = 0; j < SIZE; ++j) {
                image[i][j] /= 2;
            }
        }
    }
    else {

        for (int i = 0; i < SIZE; ++i) {
            for (int j = 0; j < SIZE; ++j) {
                image[i][j] += (255 - image[i][j]) / 2;
            }
        }
    }


}
void blackandwhite(){
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j< SIZE; j++) {
            if (image[i][j] > 127)
                image[i][j] = 255;
            else
                image[i][j] = 0;
        }
    }
}
void invert (){
    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            image[i][j]=255-image[i][j];
        }
    }
}
void merge(){
    char imageFileName[100];

    // Get gray scale image file name
    cout << "Please enter name of image file to merge with:  ";
    cin >> imageFileName;

    // Add to it .bmp extension and load image
    strcat (imageFileName, ".bmp");
    readGSBMP(imageFileName, image2);

    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            image[i][j]=(image2[i][j]+image[i][j])/2;
        }
    }
}


int main()
{
    loadImage();
    doSomethingForImage();
    return 0;
}

//_________________________________________
void loadImage () {
    char imageFileName[100];

    // Get gray scale image file name
    cout << "Please enter file name of the image to process: \n";
    cin >> imageFileName;

    // Add to it .bmp extension and load image
    strcat (imageFileName, ".bmp");
    readGSBMP(imageFileName, image);
}

//_________________________________________
void saveImage () {
    char imageFileName[100];

    // Get gray scale image target file name
    cout << "Enter the target image file name: ";
    cin >> imageFileName;

    // Add to it .bmp extension and load image
    strcat (imageFileName, ".bmp");
    writeGSBMP(imageFileName, image);
}

//_________________________________________
void doSomethingForImage() {
    while(true) {
        cout << "Please select a filter to apply or 0 to exit:\n";
        cout <<  "1-Black & White Filter\n"
                "    2-Invert Filter\n"
                "    3-Merge Filter\n"
                "    4-Flip Image\n"
                "    5-Darken and Lighten Image\n"
                "    6-Rotate Image\n"
                "    s- Save the image to a file\n"
          "           0-Exit\n";

        char s;
        cin >> s;
        if (s == '1') {
            blackandwhite();
        } else if (s == '2') {
            invert();
        } else if (s == '3') {
            merge();
        }
        else if (s=='s'){
            saveImage();
        }
        else if (s == '0') {
            break;
        }
    }


}
