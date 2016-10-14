# ajax

function createAjax() {
            var ajaxHttp = null;
            try {
                if (typeof ActiveXObject == 'function')
                    ajaxHttp = new ActiveXObject("Microsoft.XMLHTTP");
                else
                    if (window.XMLHttpRequest)
                        ajaxHttp = new XMLHttpRequest();
            }
            catch (e) {
                alert(e.message);
                return null;
            }
            return ajaxHttp;
        };

        function sendAjax(method, url, data, cfunc) {
            if (!method)
                method = 'GET';
            if (!data)
                data = null;
            var AJAXobj = createAjax();
            AJAXobj.onreadystatechange = function () {
                if (AJAXobj.readyState === 4 && AJAXobj.status === 200) {
                    if (cfunc)
                        cfunc(this);
                }
            };

            AJAXobj.open(method, url, true);
            AJAXobj.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
            AJAXobj.send(data);
        }
