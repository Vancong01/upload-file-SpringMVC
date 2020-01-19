# upload-file-SpringMVC
#sử dụng cookie
# Khi lưu ảnh, ảnh sẽ lưu trong thư mục ở đường dẫn trong máy của bạn: C:\Users\laptop\Documents\JAVABOOTCAMP\shop_images
#file để lưu file ảnh ở : global_config_app.properties
#Phải cấu hình trong Bean:
//1.Config FileUpload
    @Bean(name = "multipartResolver")
    public CommonsMultipartResolver getResolver() throws IOException {
        CommonsMultipartResolver resolver = new CommonsMultipartResolver();

        //Set the maximum allowed size (in bytes) for each individual file.
        resolver.setMaxUploadSizePerFile(5242880);//5MB

        //You may also set other available properties.

        return resolver;
    }
//2.  Cấu hình để sử dụng các file nguồn tĩnh (html, image, ..)
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {

        String fileUpload = env.getProperty("file_upload").toString();

        // Image resource.
        registry.addResourceHandler("/i/**") //
                .addResourceLocations("file:" + fileUpload);


        // Css resource.
        registry.addResourceHandler("/styles/**") //
                .addResourceLocations("/WEB-INF/resources/css/");

    }
