<template>
    <div>
        <div id="map" style="width:750px;height:750px;"></div>
        <button>버튼1</button>
    </div>

</template>

<script>
    import loadScriptOnce from 'load-script-once';
    export default {
        name: "Map",
        data() {
            return {
                infowindow: "",
                mapContainer: "",
                map: "",
                ps: "",
                mapOption: "",
                zoomControl: "",
                marker: "",
                place:"",
                bounds: "",
            }
        },
        mounted() {
            // loadScriptOnce(`//dapi.kakao.com/v2/maps/sdk.js?appkey=7c8b78578a123cad363d0029fc147776&libraries=services`)
            // .then(() => {
            //     this.openKakakoMap()
            // })
            this.openKakakoMap()
        },
        methods: {
            openKakakoMap() {
                console.log( "__KENNY__ openKakakoMap()")

                // 마커를 클릭하면 장소명을 표출할 인포윈도우 입니다
                this.infowindow = new kakao.maps.InfoWindow({zIndex: 1});

                // 지도를 표시할 div
                this.mapContainer = document.getElementById('map')
                this.mapOption = {
                        center: new kakao.maps.LatLng(37.401470, 127.108642), // 지도의 중심좌표
                        level: 3 // 지도의 확대 레벨
                    };

                // 지도를 생성합니다
                this.map = new kakao.maps.Map(this.mapContainer, this.mapOption);

                // 지도에 확대 축소 컨트롤을 생성한다
                this.zoomControl = new kakao.maps.ZoomControl();
                //
                // // 지도의 우측에 확대 축소 컨트롤을 추가한다
                this.map.addControl(this.zoomControl, kakao.maps.ControlPosition.RIGHT);

                // 장소 검색 객체를 생성합니다
                this.ps = new kakao.maps.services.Places();

                // 키워드로 장소를 검색합니다
                this.ps.keywordSearch('판교 맛집', this.placesSearchCB);
            },
            placesSearchCB(data, status, pagination) {
                console.log( '__KENNY__ placesSearchCB() START!!')

                if (status === kakao.maps.services.Status.OK) {

                    // 검색된 장소 위치를 기준으로 지도 범위를 재설정하기위해
                    // LatLngBounds 객체에 좌표를 추가합니다
                    this.bounds = new kakao.maps.LatLngBounds();

                    for (let i = 0; i < data.length; i++) {
                        console.log( '__KENNY__ data[i] : ' )
                        console.log( data[i] )

                        this.displayMarker(data[i]);
                        this.bounds.extend(new kakao.maps.LatLng(data[i].y, data[i].x));
                    }

                    // 검색된 장소 위치를 기준으로 지도 범위를 재설정합니다
                    this.map.setBounds(this.bounds);
                }
            },
            displayMarker(data) {
                console.log( '__KENNY__ displayMarker() START!!' )
                console.log( data )

                // 마커를 생성하고 지도에 표시합니다
                let marker1 = new kakao.maps.Marker({
                    map: this.map,
                    position: new kakao.maps.LatLng(data.y, data.x)
                });

                // 마커에 클릭이벤트를 등록합니다
                kakao.maps.event.addListener(marker1, 'click', () => {
                    console.log( '__KENNY__ clickMarker() START!!')
                    console.log( data )

                    // 마커를 클릭하면 장소명이 인포윈도우에 표출됩니다
                    this.infowindow.setContent('<div style="padding:5px;font-size:12px;">' + data.place_name + '</div>');
                    this.infowindow.open(this.map, marker1);
                });
            },

        }
    }
</script>

<style scoped>

</style>
