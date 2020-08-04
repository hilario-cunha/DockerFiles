# docker-msbuild-cf
To create a docker image that can do msbuild of csharp compact framework projects

# Example to create the image:
docker build . -t msbuild-cf:1.0

# Example to run the image:
docker run -it msbuild-cf:1.0
