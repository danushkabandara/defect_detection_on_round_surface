gray_image = rgb2gray(imread('..\images\15R_207_COLOR2D.jpg'));
I = imbinarize(gray_image, 0.3);
se = strel('line',8,8);
gray_image = imdilate(gray_image,se);

%se = strel('line',15,15);


gray_image = imerode(gray_image,se);


imshow(gray_image)

[centers, radii, metric] =imfindcircles(I,[350,370],'Sensitivity',.98);

centersStrong5 = centers(1:1,:); 
radiiStrong5 = radii(1:1);
metricStrong5 = metric(1:1);

viscircles(centersStrong5, radiiStrong5,'EdgeColor','b');
theta=-pi:0.005:pi;%you can increase this if this isn't enough yet
intensity_array = zeros(length(theta));



for j =5:6
    radius= radii(1)-j
    x=centers(1,1)+radius*cos(theta);
    y=centers(1,2)+radius*sin(theta);
    
    for i = 1:length(theta)
        int_x =  round(x(1,i));
        int_y = round(y(1,i));
        %plot(int_x, int_y,'rd','MarkerSize',3)
        if gray_image(int_x,int_y)>0
            intensity_array(i) = intensity_array(i)+gray_image(int_x,int_y);
        end
       
    end
end
plot(rad2deg(theta),intensity_array)

imshow(I);
%hold on;
j=1
for i = 1:length(x)
   if round(intensity_array(i))>0
      % plot((centers(1,1)+radius*cos(-3.14+6.28*i/length(theta))), (centers(1,2)+radius*sin(-3.14+6.28*i/length(theta))),'rd','MarkerSize',intensity_array(i))
       j = j+1;
   end
    
end


moving_var = movvar(intensity_array,5);
moving_var_tr=transpose(moving_var(:,1));
plot(rad2deg(theta),moving_var)
hold on
[PKAmp,PKTime]=findpeaks(moving_var_tr,rad2deg(theta),'MinPeakProminence', 400, 'MinPeakDistance', 20);
plot(PKTime, PKAmp, '^r', 'MarkerFaceColor','r')
hold off


imshow(gray_image)
hold on
for i = 1:length(PKTime)
       plot(centers(1,1)+radius*cos(3.14/2-1*deg2rad(PKTime(i))), centers(1,2)+radius*sin(3.14/2-1*deg2rad(PKTime(i))),'rd','MarkerSize',5);
    
       end


