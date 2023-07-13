function convertNumbers2English (string) {
    return string.replace(/[\u0660-\u0669]/g, function (c) {
        return c.charCodeAt(0) - 0x0660;
    }).replace(/[\u06f0-\u06f9]/g, function (c) {
       return c.charCodeAt(0) - 0x06f0;
   });
}

function getEventsMonth(){

var listEvent = {};

$(".eventsCurrentMonthWrapper ul li").each((i , element) => { 

const numberOfDay = parseInt(convertNumbers2English($(element).find("span:first").text()).replace(/\D/gi , ""));
listEvent[numberOfDay] = listEvent[numberOfDay] ?? [];

$(element).find("span:first").remove();
listEvent[numberOfDay].push($(element).text().replace(/\s{2,}/gi , ""));

});

return listEvent;
}

var listEvent = getEventsMonth();
var list = [];

$(".dayList > div").each((i , element) => {
	var counter = -1;
	
	let isDisabled = true;
	
	if(!$(element).hasClass("disabled")){
		counter = Number(convertNumbers2English($(element).find(".jalali").text()));
		isDisabled = false;
	}
	
	list.push([
	$(element).find(".jalali").text(),
	$(element).find(".miladi").text(),
	$(element).find(".qamari").text(),
	$(element).find(".holiday").length == 0 ? false : true,
	listEvent[counter] ?? [],
	isDisabled
	])
})

JSON.stringify(list);