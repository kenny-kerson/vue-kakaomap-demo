<template>
    <div id="map" style="width:750px;height:750px;"></div>
</template>

<script>
    export default {
        name: "Map",
        mounted() {
            this.openKakakoMap()
        },
        methods: {
            openKakakoMap() {
                var container = document.getElementById('map'); //지도를 담을 영역의 DOM 레퍼런스
                var options = { //지도를 생성할 때 필요한 기본 옵션
                    center: new kakao.maps.LatLng(37.56682, 126.97865),
                    level: 3,
                    mapTypeId : kakao.maps.MapTypeId.ROADMAP,
                };

                var map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴

                // 지도에 확대 축소 컨트롤을 생성한다
                var zoomControl = new kakao.maps.ZoomControl();

                // 지도의 우측에 확대 축소 컨트롤을 추가한다
                map.addControl(zoomControl, kakao.maps.ControlPosition.RIGHT);

                var marker = new kakao.maps.Marker({
                    position: new kakao.maps.LatLng(37.56682, 126.97865), // 마커의 좌표
                    map: map // 마커를 표시할 지도 객체
                });
            }
        }
    }
</script>

<style scoped>

</style>
