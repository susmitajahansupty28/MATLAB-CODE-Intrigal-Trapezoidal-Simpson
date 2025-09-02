# MATLAB-CODE-Intrigal-Trapezoidal-Simpson
 
function Intrigal_Trapezoidal_Simpson()
f = @(x) 1./(1+x.^2);   % Main function (প্রশ্নে যে ফাংশনটা দেওয়া থাকবে, এখানে লিখলেও হবে আবার না লিখলেও রান করবে। তবে লিখা ভালো)

% Parameters :
% a = 0;    Lower limit
% b = 1;    Upper limit
% n = 6;    Number of subintervals (must be even for Simpson's 1/3)

% অথবা এখানে সব গুলো ভ্যালু ইনপুট হিসেবেও নিতে পারো ভিন্ন ভিন্ন ফাংশনের জন্য:
a = input('Enter lower value a: ');
b = input('Enter upper value b: ');
n = input('Enter Number of subintervals n: ');



% Run Methods: এর মানে ডিসপ্লে তে কিভাবে শো করবে সেটা।
% আগে মেথডের নাম প্রিন্ট হবে তারপর রুট বা রেজাল্ট দেখাবে।
% Trapezoidal আর simpson ফাংশনের নিউম্যারিকেল ভ্যালুগুলো T,S3 & S8 তে রাখা হয়েছে যেনো পরের বার আলাদা ভাবেও ফাইনাল রেজাল্ট মনিটরে চিহ্নিত করা যায়।

fprintf('Integrating f(x) = 1/(1+x^2) from %d to %d\n', a, b);

% Trapezoidal Rule
T = trapezoidal(f, a, b, n);
fprintf('\n1. Trapezoidal Rule Result: %.6f\n', T);

% Simpson's 1/3 Rule
S3 = simpson_one_third(f, a, b, n);
fprintf('2. Simpson''s 1/3 Rule Result: %.6f\n', S3);

% Simpson's 3/8 Rule 
S8 = simpson_three_eighth(f, a, b, n);
fprintf('3. Simpson''s 3/8 Rule Result: %.6f\n', S8 );

% Exact value (for comparison)
exact = atan(1) - atan(0);         % ∫ 0→1 1/(1+x^2) dx = arctan(1)-arctan(0)=pi/4
fprintf('\nExact Integral Value = %.6f\n', exact);




% Trapezoidal আর simpson ফাংশনের নিউম্যারিকেল ভ্যালুটা প্রতিবার I তে থাকব
% All 3 Functions:

function I = trapezoidal(f, a, b, n) 
    h = ((b-a)/n);
    x = a:h:b;
    y = f(x);
    I = (h/2)*(y(1) + 2*sum(y(2:end-1)) + y(end));
end





function I = simpson_one_third(f, a, b, n)
    if mod(n,2) ~= 0
        error('n must be even for Simpson 1/3 rule');
    end
    h = (b-a)/n;
    x = a:h:b;
    y = f(x);
    I = (h/3)*(y(1) + 4*sum(y(2:2:end-1)) + 2*sum(y(3:2:end-2)) + y(end));   
end





function I = simpson_three_eighth(f, a, b, n)
    if mod(n,3) ~= 0
       error('n must be multiple of 3 for Simpson 3/8 rule');
    end
    h = (b-a)/n;
    x = a:h:b;
    y = f(x);
    I = (3*h/8)*(y(1) + 3*sum(y(2:3:end-1)) + 3*sum(y(3:3:end-1)) + 2*sum(y(4:3:end-3)) + y(end));   
end




    % যদি Trapezoidal প্লট আকতে চাও তবে এই নিচের কোড গুলো এড করতে হবেঃ
    figure;
    subplot(2,2,1);
    x = linspace(a,b,200);
    plot(x,f(x),'b','LineWidth',1.5);
    title('Trapezoidal Rule Approximation');
    hold on; grid on;

    area(linspace(a,b,n+1), f(linspace(a,b,n+1)), 'FaceAlpha',0.2,'EdgeColor','r');

    
    
    % যদি Simpson 1/3 প্লট আকতে চাও তবে এই নিচের কোড গুলো এড করতে হবে
    subplot(2,2,2);
    x = linspace(a,b,200);
    plot(x,f(x),'b','LineWidth',1.5);
    title('Simpson 1/3 Rule Approximation');
    hold on; grid on;

    xx = linspace(a,b,n+1); yy = f(xx);
    plot(xx,yy,'ro-','LineWidth',1.2);

    
    
    % যদি Simpson 3/8 প্লট আকতে চাও তবে এই নিচের কোড গুলো এড করতে হব    
    subplot(2,2,3);
    x = linspace(a,b,200);
    plot(x,f(x),'b','LineWidth',1.5);
    title('Simpson 3/8 Rule Approximation');
    hold on; grid on;

    xx = linspace(a,b,n+1); yy = f(xx);
    plot(xx,yy,'gs-','LineWidth',1.2);
end

 
