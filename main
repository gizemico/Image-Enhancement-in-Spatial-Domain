%% Decode the encoded text in the image

clear all;clc;

%read the image from the file.
img=imread('EncodedImage.png');

%show encoded image.
figure; imshow(img),title('encoded image');

%find row and column size seperately.
row=size(img,1);
column=size(img,2);

%find the array's size which equals pixels.
pix=(row)*(column);

%convert from double to integer.
output=uint8(zeros(row,column));


%create the arrays for occurence, probabilities, sum of occurence, output.
oc_val=zeros(256,1);
pf=zeros(256,1);
pc=zeros(256,1);
c=zeros(256,1);
final=zeros(256,1);

%intensity level, (L-1)=(2^8)-1=255.
intensity=255;

for x=1:row
    for y=1:column
        %calculate the histogram processing.
        pix_val=img(x,y); %find the pixel's values for every point.
        oc_val(pix_val+1)=oc_val(pix_val+1)+1;%count this value to the array(occurence number).
        
        %calculate the normalized.
        %divide all occurence numbers by size of image(number of pixels).
        pf(pix_val+1)=oc_val(pix_val+1)/pix; 
    end
end

sum=0;

for x=1:size(pf)
    sum=sum+oc_val(x);%find the sum of occurence number.
    c(x)=sum; %add the sum values to the array.
    pc(x)=c(x)/pix; %divide the sum values by size of image(number of pixels).
    final(x)=round(pc(x)*intensity); %rounded from float numbers to integers if not an integer type.
     %and find the histogram equalization.
end


for x=1:row
    for y=1:column
        output(x,y)=final(img(x,y)+1); %generate the output image.
    end
end

imwrite(output,'DecodedImage.png');

%display the final image and write title.
figure; imshow(output),title('DecodedImage');

%% Enhance the quality of image by removing the noise

clear all;clc;

%read the image from the file.
img=imread('NoisyImage.png');

%show the image.
subplot(1,2,1); imshow(img),title('noisy image');

%find size of row and column.
 row=size(img,1);
 column=size(img,2);
 
%padding.
pad=uint8(zeros(row+2,column+2));
pad(2:row+1,2:column+1)=img; %starts with 2, because after enlarge with pad our image will start pixel of (2,2).

%create matrices.
arr=zeros(3,3);
output=uint8(zeros(row,column));
new=zeros(1,9);

for i=2:1:row+1 %starts with 2, and ended with row+1 because after padding, original image inside pad. 
     for j=2:1:column+1 %starts with 2, and ended with column+1 because after padding, original image inside pad. 
         
         arr(1,1)= pad(i-1,j-1);
         arr(2,1)= pad(i,j-1);
         arr(3,1)= pad(i+1,j-1);
         arr(1,2)= pad(i-1,j);
         arr(2,2)= pad(i,j);
         arr(3,2)= pad(i+1,j);
         arr(1,3)= pad(i-1,j+1);
         arr(2,3)= pad(i,j+1);
         arr(3,3)= pad(i+1,j+1);
        
         x=sort(arr(1,:)); %sort for first row.
         y=sort(arr(2,:)); %sort for second row.
         z=sort(arr(3,:)); %sort for third row.
         new=[x,y,z]; %combine the sorted rows(x,y and z).
         s=sort(new); %sort the new combining array.
         output(i-1,j-1)=s(5); %write the median value in output matrix.
     end
end

%write the image to file.
imwrite(output,'EnhancedImage.png');

%show the enhanced image with its title.
subplot(1,2,2); imshow(output),title('enhanced image');
       
        
%% Enhance the quality of image by removing the blur

clear all; clc;

%read the image from the file.
img=imread('BlurImage.png');

%show the blur image.
figure; imshow(img),title('blur image');

%filter with size 3x3.
F=[1 1 1 ; 1 -8 1 ; 1 1 1];

%seperate the filter for every column.
F1=(F(:,1));
F2=(F(:,2));
F3=(F(:,3));

%find size of row and column.
 row=size(img,1);
 column=size(img,2);
 
%create the array.
 arr=zeros(3,3);
 output=uint8(zeros(row,column));
 sharpened=uint8(zeros(row,column));
 
%padding.
pad=(zeros(row+2,column+2));

%after creating pad, original image should start in (2,2) point's.
pad(2:row+1,2:column+1)=img;

for i=2:1:row+1 %row starts our original image's pixels in padding.
    for j=2:1:column+1%column starts our original image's pixels in padding.
       
        %padding
        arr(1,1)=pad(i-1,j-1);
        arr(1,2)=pad(i-1,j);
        arr(1,3)=pad(i-1,j+1);
        arr(2,1)=pad(i,j-1);
        arr(2,2)=pad(i,j);
        arr(2,3)=pad(i,j+1);
        arr(3,1)=pad(i+1,j-1);
        arr(3,2)=pad(i+1,j);
        arr(3,3)=pad(i+1,j+1);
        
        a1=(arr(1,:)); %seperate for first row.
        a2=(arr(2,:)); %seperate for second row.
        a3=(arr(3,:)); %seperate for third row.        
        
        m=(a1*F1)+(a2*F2)+(a3*F3);%multiply of matrices.
        output(i-1,j-1)=m;
        
    end
end

sharpened=img-output; %subtract output from original image, find the sharpening image.

figure;imshow(output),title('laplace image');

%write the image to file.
imwrite(sharpened,'EnhancedImage2.png');
figure;imshow(sharpened),title('EnhancedImage2.png');
