<p align="center">
<img src="src/frontend/static/icons/Hipster_HeroLogoMaroon.svg" width="300" alt="Online Boutique" />
</p>

# Setting up Online Boutique with Choreo 

> **Note:**
    This is fork from the [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo) repository and additional changes are included in order to deploy the application on [Choreo](https://wso2.com/choreo/).

# Step 1: Create and Deploy Services

You will create the services that the web application needs to consume. Before you proceed, sign into [**Choreo Console**](https://console.choreo.dev/).

## Step 1.1: Create and Deploy the Email Service

Let's create your first Service.
1. On the **Home** page, click on the project you created.
2. Click **Create** in the Service card.
3. Enter a unique name and a description for the Service. For example, you can enter the name and the description given below:

    | Field | Value |
    | -------- | -------- |
    | Name | Email Service |
    | Description | Send Emails. |

4. Click **Next**.
5. To allow Choreo to connect to your GitHub account, click **Authorize with GitHub**.
6. If you have not already connected your GitHub repository to Choreo, enter your GitHub credentials, and select the repository you created by forking https://github.com/wso2/microservices-demo to install the Choreo GitHub App.
7. In the Connect Repository dialog box, enter the following information:

    | Field | Value |
    | -------- | -------- |
    | GitHub Account | Your account |
    | GitHub Repository | microservices-demo |
    | Branch | main |
    | Build Preset | Click **Dockerfile**  |
    | Dockerfile Path | /src/emailservice/Dockerfile |
    | Docker Context Path | /src/emailservice|

8. Click **Create** to initialize a Service with the implementation from your GitHub repository.
9. The Service opens on a separate page where you can see deploy details.
10. Click **Deploy Manually** on the **Build Area** to deploy the service.
11. Navigate to the **Overview** area after the service has been successfully deployed. The internal **endpoint** of the service is something like http://email-service-3192360657:8080/. Make a note of the endpoint value for future reference.


## Step 1.2: Create and Deploy other Services

1. Follow the steps in **step 1.1** and create the services with the following information. 

    | Service Name     | Dockerfile Path |  Docker Context Path |
    | ---------------- | --------------- |  ------------------- |
    | Currency Service | /src/currencyservice/Dockerfile | /src/currencyservice |
    | Product Catalog Service | /src/productcatalogservice/Dockerfile | /src/productcatalogservice |
    | Shipping Service | /src/shippingservice/Dockerfile | /src/shippingservice |
    | Ad Service | /src/adservice/Dockerfile | /src/adservice |
    | Payment Service | /src/paymentservice/Dockerfile | /src/paymentservice |
    | Cart Service | /src/cartservice/src/Dockerfile | /src/cartservice/src |
    | Recommendation Service | /src/recommendationservice/Dockerfile | /src/recommendationservice |
    | Checkout Service | /src/checkoutservice/Dockerfile | /src/checkoutservice | 

2. The below services are having environment variables. Follow the below steps to add environment variables.

- Navigate to **Configs & Secrets** section on the left navigation menu in the **Deploy** section.
- Click **Create**.
- Select config type as **ConfigMap** and mount type as **Environment Variables**. Then click **Next**.
- Provide the following information and click **Create**. Use the **host** and **port** of the internal **endpoints** of the services as environment variables. eg: If the internal endpoint is http://email-service-3192360657:8080/, then environment variable value should be **email-service-3192360657:8080**.

   - Recommendation Service 

      | Environment Variable Name     | Environment Variable Value |
      | ---------------- | --------------- | 
      | PRODUCT_CATALOG_SERVICE_ADDR | Product catalog service endpoint. eg: product-catalog-service-3192360657:3550 |

   - Checkout Service 

      | Environment Variable Name     | Environment Variable Value |
      | ---------------- | --------------- | 
      | PRODUCT_CATALOG_SERVICE_ADDR | Product catalog service endpoint. eg: product-catalog-service-3192360657:3550 |
      | SHIPPING_SERVICE_ADDR | Shipping service endpoint. eg: shipping-service-3192360657:3550 |
      | PAYMENT_SERVICE_ADDR | Payment service endpoint. eg: payment-service-3192360657:50051 |
      | EMAIL_SERVICE_ADDR | Email service endpoint. eg: email-service-3192360657:8080 |
      | CURRENCY_SERVICE_ADDR | Currency service endpoint. eg: currency-service-3192360657:7000 |
      | CART_SERVICE_ADDR | Cart service endpoint. eg: cart-service-3192360657:7070 |

3. After adding environment variables, you can click **Deploy Manually** on the **Build Area** to deploy the services.

&nbsp;<br>
# Step 2: Create and Deploy the front-end application

## Step 2.1: Configure the front-end application

1. Navigate to **Choreo Console**.
2. Navigate to the **Components** section from the left navigation menu.
3. Click on the **Create** button.
4. Click on the **Create** button in the **Web Application** Card.
5. Enter a unique name and a description for the Web Application. For example you can provide the following sample values.

    | Field | Value |
    | -------- | -------- |
    | Name | Front-end Web App |
    | Description | Front-end application |

6. Click on the **Next** button.
7. To allow Choreo to connect to your **GitHub** account, click **Authorize with GitHub**.
8. In the Connect Repository dialog box, enter the following information:

    | Field | Value |
    | -------- | -------- |
    | GitHub Account | Your account |
    | GitHub Repository | microservices-demo |
    | Branch | main |
    | Dockerfile Path | /src/frontend/Dockerfile |
    | Docker Context Path | /src/frontend|
    | Port |8080|

9. Click on the **Create** button.
10. The Web Application opens on a separate page where you can see its overview.

## Step 2.2: Add environment variables for the front-end application

1. Navigate to **Configs & Secrets** section on the left navigation menu in the **Deploy** section.
2. Click **Create**.
3. Select config type as **ConfigMap** and mount type as **Environment Variables**. Then click **Next**.
4. Provide the following information and click **Create**.

      | Environment Variable Name     | Environment Variable Value |
      | ---------------- | --------------- | 
      | PRODUCT_CATALOG_SERVICE_ADDR | Product catalog service endpoint. eg: product-catalog-service-3192360657:3550 |
      | SHIPPING_SERVICE_ADDR | Shipping service endpoint. eg: shipping-service-3192360657:3550 |
      | CURRENCY_SERVICE_ADDR | Currency service endpoint. eg: currency-service-3192360657:7000 |
      | CART_SERVICE_ADDR | Cart service endpoint. eg: cart-service-3192360657:7070 |
      | RECOMMENDATION_SERVICE_ADDR | Recommendation service endpoint. eg: recommendationservice-3192360657:8080 |
      | CHECKOUT_SERVICE_ADDR | Checkout service endpoint. eg: checkoutservice-3192360657:5050 |
      | AD_SERVICE_ADDR | Ad service endpoint. eg: adservice-3192360657:9555 |

## Step 2.3: Deploy the front-end application

1. Navigate to **Build and Deploy** section on the left navigation menu.
2. Click **Deploy Manually** on the **Build Area**.
3. When the application is deployed successfully you will get an url in the section **Web App URL**.

&nbsp;<br>
# Step 3: Consume the Application

You can use the **Web App URL** to access the **Online Boutique** application.


| Home Page                                                                                                         | Checkout Screen                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [![Screenshot of store homepage](./docs/img/online-boutique-frontend-1.png)](./docs/img/online-boutique-frontend-1.png) | [![Screenshot of checkout screen](./docs/img/online-boutique-frontend-2.png)](./docs/img/online-boutique-frontend-2.png) |

--------