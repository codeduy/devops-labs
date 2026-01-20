## Check log container
```
docker logs <CONTAINER ID>
```

## Check info container bao gồm các thông tin config, network, volume mount point,...
```
docker inspect <CONTAINER ID>
```

## Xem trạng thái tài nguyên đang sử dụng của toàn bộ các container hoặc 1 container được chỉ định
```
docker stats
```
```
docker stats <CONTAINER ID>
```

## Xóa container
```
docker rm -f <CONTAINER ID>
```

## Build image từ thư mục chứa Dockerfile
```
docker build -t <tên_image>
```

## Chạy container từ image
```
docker run -d -p <host_port>:<container_port> --name <tên> <image>
```

## Truy cập vào container để thực thi command
```
docker exec -it <container_id> sh
```

## Xem danh sách container
```
docker ps
```

## Xem danh sách image
```
docker images
```

## Xóa image (yêu cầu xóa container thuộc image đó trước)
```
docker rmi <image_id>
```

## Xóa những thứ không còn dùng (bao gồm stop container, network, cache)
```
docker system prune
```
> Ở cách này sẽ đảm bảo giải phóng dung lượng trống cho ổ cứng nhưng cần có sẵn remote cache để khi chạy build image sẽ tránh tốn thời gian cho lần build sau (remote cache sẽ nằm trên registry như DockerHub,...)

