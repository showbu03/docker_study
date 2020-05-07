# test1

문자, 숫자 판단

```
if('1' <= str.charAt(i) <= '9')
if('A' <= str.charAt(i) <= 'z')
```

리스트 정렬

```text
list.add(Integer.parseInt(list.get(i)));
Collections.sort(List);
// or
Collections.sort(integerList,Collections.reverseOrder());
Integer.toString(List.get(0));
Integer.toString(List.get(list.size()-1));
return Math.max(num1, num2);
```

문자 숫자만큼 출력
```text
char last = '\n';
for (char c : inputData.toCharArray()) {
	if (c >= '2' && c <= '9') {
		for (int i = 1; i < Integer.parseInt(Character.toString(c)); i++) {
			result += last;
		}
	} 
	else if (c != '\n') {
		result += c;
	} 
	last = c;
}
```

카드/ 문자열 판별
```text
String preCard = "";
for(int i=0; i < inputData.length; i++) {
	if( i > 0 ) {
		if(preCard.charAt(0) != inputData[i].charAt(0) &&
		   preCard.charAt(1) != inputData[i].charAt(1)) {
			System.out.println("not a rule at index=" + i);
			return false;
		}
	}
	preCard = inputData[i];
}
```

배열 가로행 합
```text
int[][] summedData = null;

///////////////////////
summedData = new int[inputData.length][inputData[0].length+1];

for(int i=0; i < inputData.length; i++) {
	int nSum = 0;
	for(int j = 0; j < inputData[0].length; j++) {
		summedData[i][j] = inputData[i][j];
		nSum += inputData[i][j];
	}
	summedData[i][inputData[0].length] = nSum;
}

중앙 열을 기준으로 좌우 교환한 후, 세로(열)의 합을 추가하는 기능
int[][] resultData = null;

///////////////////////
resultData = new int[summedData.length+1][summedData[0].length];
int halfLength = (int)(summedData[0].length / 2);
//System.out.println("halfLength=" + halfLength);

int[] columnSum = new int[summedData[0].length];

for(int i=0; i < summedData.length; i++) {
	for(int j = 0; j < summedData[0].length; j++) {

		int column = 0;
		if( summedData[0].length%2 == 1 ) {  // 홀수일때
			if(j == halfLength) {
				column = j;
			} else if(j > halfLength) {
				column = j - halfLength - 1;
			} else {
				column = j + halfLength + 1;
			}

		} else {  // 짝수일때

			if(j >= halfLength) {
				column = j - halfLength;
			} else {
				column = j + halfLength;
			}
		}

		resultData[i][j] = summedData[i][column];

		columnSum[j] += resultData[i][j];
	}
}	

for(int j = 0; j < summedData[0].length; j++) {
	resultData[summedData.length][j] = columnSum[j];
}

////////////////////////////
```

키패드

```text
boolean valid = true;

///////////////////////
if (inputData == null || inputData.length() < 6 || inputData.length() > 15) {
	System.out.println("length error.");
	return false;
}
for (int i = 0; i < inputData.length(); i++) {
	if (inputData.charAt(i) < '0' || inputData.charAt(i) > '9') {
		System.out.println("not number error.");
		return false;
	}
}

String[] prohibit = { "123", "456", "789", "321", "654", "987", "147", "258", "369", "741", "852", "963", "159",
		"951", "357", "753", "025", "520" };

for (int j = 0; j < prohibit.length; j++) {
	if (inputData.indexOf(prohibit[j]) >= 0) {
		System.out.println("prohibit error. ==> " + prohibit[j]);
		return false;
	}
}
////////////////////////////

동일한숫자를연속3회이상입력할수는없다 (입력으로*, #이들어오는경우는없음)
전체패스워드중동일패턴(2자리이상)이연속존재할수없다. (입력으로*, #이들어오는경우는없음)
boolean valid = true;
//////////////////////// 여기부터 코딩 (2) ---------------->
for(int i = 0; i < inputData.length(); i++) {
	if( i >= 2) {
		if(inputData.charAt(i) == inputData.charAt(i-1) &&
		   inputData.charAt(i) == inputData.charAt(i-2)) {
			System.out.println("same three char error.");
			return false;
		}
	}
}

for(int i = 0; i <= inputData.length(); i++) {
	if( i >= 4) {
		if(inputData.substring(i-2, i).equals(inputData.substring(i-4,i-2)) ) {
			System.out.println("same pattern error.");
			return false;
		}
	}
	if( i >= 6) {
		if(inputData.substring(i-3, i).equals(inputData.substring(i-6,i-3)) ) {
			System.out.println("same pattern error.");
			return false;
		}
	}	
	if( i >= 8) {
		if(inputData.substring(i-4, i).equals(inputData.substring(i-8,i-4)) ) {
			System.out.println("same pattern error.");
			return false;
		}
	}	
	if( i >= 10) {
		if(inputData.substring(i-5, i).equals(inputData.substring(i-10,i-5)) ) {
			System.out.println("same pattern error.");
			return false;
		}
	}	
	if( i >= 12) {
		if(inputData.substring(i-6, i).equals(inputData.substring(i-12,i-6)) ) {
			System.out.println("same pattern error.");
			return false;
		}
	}				
}		

///////////////////////////// <-------------- 여기까지 코딩 (2)
		
```
2차원 배열 행단위 정열

```text
for(int r=0; r<n; r++)
Arrays.sort(arr[r]);
```

2차원 배열 열단 정열

```text
for(int c=0; c<n; c++) {
 int[] tmpArr = new int[N];
 for(int r=0; r<n; r++){
  tmpArr[r] = arr[r][c];
 }
 Arrays.sort(tmpArr);
 for(int r=0; r<n; r++) {
   arr[r][c] = tmpArr[r];
 }
}
```

2차원 배열 인접한 대상 찾기\(상하, 좌우\)

```text
int  totlasum = 0;
for(int r=0; r<n; r++) {
  for(int c=0; c<n; c++) {
    boolean isSame = false;
   if(r > 0 && arr[r][c] == arr[r-1][c]) // 위   
      isSame = true;
   if(r > 0 && arr[r][c] == arr[r+1][c]) // 아래   
      isSame = true;
   if(r > 0 && arr[r][c] == arr[r][c-1]) // 왼쪽
      isSame = true;
   if(r > 0 && arr[r][c] == arr[r][c+1]) // 왼쪽
      isSame = true;
      
   if(!isSame){
     totlasum += arr[r][c];
   }
  }
}
```

문자 포함여부 체크

```text
if( str.indexOf(".") > -1 ) 
//마지막 인덱스 정보를 기준으로 문자열 자르기
data.substring(0, str.lastIndexOf("."));



```

파일/디렉토리수 계산

```text
for (String filePath : inputData) {
	if (!filePath.endsWith("/")) {
		numOfFiles ++;
	}
}

Set<String> dirSet = new HashSet<String>();		
for (String path : inputData) {
	while (path.indexOf('/')>=0) {
		path = path.substring(0, path.lastIndexOf('/'));				
		dirSet.add(path);			
	}
}		
numOfDir = dirSet.size();

```
```text
	secondCodeNameList = new ArrayList<String>();
		for(String data:firstCodeNameList){
			String tmp = data.substring(0, data.lastIndexOf("."));
			
			if(tmp.indexOf("a")>-1 || tmp.indexOf("x")>-1){
				if(tmp.indexOf("ax")>-1 || tmp.indexOf("ab")>-1 || tmp.indexOf("xy")>-1){
					secondCodeNameList.add(data);
				}
			}else{
				secondCodeNameList.add(data);
			}
		}
```

휴일 업무시간

```text
for (List<String> dayWorks : monthWorkInfo) {
	boolean isWorkingDay = dayWorks.get(1).equals("Y");
	if (!isWorkingDay) {
		offDayWork += calDailyWork(dayWorks);
	}
}
private static final DateFormat df = new SimpleDateFormat("HH:mm");
private int calDailyWork(List<String> dayWorks) {
	long from = 0;
	String fromStr = "";
	int dayWorkingMin = 0;
	for (int i = 2; i < dayWorks.size(); i++) {
		String time = dayWorks.get(i);
		if (i % 2 == 0) {
			fromStr = time;
			from = toTime(time);
		} else {
			long to = toTime(time);
			dayWorkingMin += (int)((to - from) / 1000 / 60);
			debug (String.format("%s - %s : %d", time,fromStr, (to - from) / 1000 / 60));
		}
	}
	return dayWorkingMin;
}

해당월 인정 M/M
public double getManMonth(List<List<String>> monthWorkInfo) {
double manMonth = 0.0;
////////////////////////
int workingDay = 0;
double monthWorks = 0.0;
for (List<String> dayWorks : monthWorkInfo) {
	if (dayWorks.get(1).equals("Y")) {
		workingDay ++;
	} else {
		continue;
	}
	int dayTimes = calDailyWork(dayWorks);
	double dayMM = 0;

	if (dayTimes < 4 * 60) {
	} else if (dayTimes < 8 *60) {
		dayMM = 0.5;
	} else {
		dayMM = 1.0;
	}
	debug ( String.format(" %2s %s %.1f %4d", dayWorks.get(0), dayWorks.get(1), dayMM , dayTimes));
	monthWorks += dayMM;
}
debug ( String.format(" %.1f %d %.2f", monthWorks, workingDay, monthWorks / workingDay));
manMonth = monthWorks / workingDay;
manMonth = Math.round(manMonth * 100.0) / 100.0; 
///////////////////////////// 

return manMonth;
}

```

부분 배열의 개수 구하기

```text
int result = 0;

for(int i=1; i<=arrSize; i++){
 result += getNumberSum(arrSize, i);
}

return result;


private int getNumberSum(int arrSize, initialNum) {
 int max=0;

 for(int i=initialNum; i<=arrSize; i++) {
   if( i <= arrSize) {
     maxX++;
   } else {
     break;
   }

 }
 return (maxX * maxX);
 }
```


각 부분 배열의 최대값 찾

```text
/**
	 * 최대값을 찾는 기능
	 *
     * @param		inputData			int[][]		입력데이터(NxN배열)
     * @return							int			최대값
	 */
	public int getMaximumValue(int[][] inputData) {
		int maximumValue = -1;
		boolean bFirst = false;
		
		////////////////////////여기부터 구현 (2) ---------------->
		for(int i=1;i<=inputData.length;i++){
			int tMaximumValue = getMaxValue(inputData,i);
			
			if ( bFirst ) {
				bFirst = false;
				maximumValue = tMaximumValue;
			} else {
				if ( maximumValue < tMaximumValue ) {
					maximumValue = tMaximumValue;
				}
			}
		}
		
		///////////////////////////// <-------------- 여기까지 구현 (2)
		return maximumValue;
	}


	private int getMaxValue(int[][] inputData, int endValue) {
		int maximumValue = 0;
		int maxLength = inputData.length;
		int orgCurrentXEnd = endValue;
		
		int currentXEnd = endValue;
		int currentYEnd = endValue;
		int currentXStart = 0;
		int currentYStart = 0;
		
		while ( maxLength >= currentXEnd ) {
			int sum = 0;
			for(int i=currentXStart;i<currentXEnd;i++){
				for(int j=currentYStart;j<currentYEnd;j++){
					sum = sum + inputData[j][i];
				}
			}
			currentXStart++;;
			currentXEnd++;
			
			if ( maximumValue < sum ) {
				maximumValue = sum;
			}
		}
		currentYStart++;
		currentYEnd++;
	
		currentXEnd = orgCurrentXEnd;
		currentXStart = 0;
		while ( maxLength >= currentYEnd ) {
			int sum = 0;
			for(int i=currentXStart;i<currentXEnd;i++){
				for(int j=currentYStart;j<currentYEnd;j++){
					sum = sum + inputData[j][i];
				}
			}
			currentXStart++;;
			currentXEnd++;
			
			currentYStart++;
			currentYEnd++;
			
			if ( maximumValue < sum ) {
				maximumValue = sum;
			}
		}
		return maximumValue;
	}
```

상위 카테고리 검색

```text
/**
	 * 상위 카테고리를 검색하는 기능
	 *
     * @param		inputData		String[][]		입력데이터(카테고리 정보)
     * @param		categories		List			입력데이터(inputCategories[0]: 카테고리1, inputCategories[1]: 카테고리2)
     * @return						String 			상위 카테고리
	 */
	public String getTopCategory(String[][] inputData, List<String> categories) {
		String topCategory = "";
		////////////////////////여기부터 구현 (1) ---------------->
		Map<String, List<String>> tMap = makeMap(inputData);		
		
		List<String> hierarchy_1 = new ArrayList<String>();
		List<String> hierarchy_2 = new ArrayList<String>();
		
		for(int i=0; i<categories.size();i++){
			for (String key : tMap.keySet()) {
				List<String> values = tMap.get(key);
				if (values.contains(categories.get(i))) {					
				    if(i == 0)
					  hierarchy_1.add(key);
				    else
				      hierarchy_2.add(key);
	
					String parent = getParent(tMap, key);
					while (!parent.isEmpty()) {
						if(i==0)
						  hierarchy_1.add(0, parent);
						else
						  hierarchy_2.add(0, parent);	
						parent = getParent(tMap, parent);
					}
				}
		    }
		}	
		
		for(String tParent:hierarchy_2){
			for(int j=0;j<hierarchy_1.size();j++){
				String oParent = hierarchy_1.get(j);
				if ( oParent.equals(tParent) ) {
					topCategory = hierarchy_1.get(j);
					break;
				}
			}
		}	
		
		
		///////////////////////////// <-------------- 여기까지 구현 (1)
		return topCategory;
	
```

하위 카테고리 개수 계산

```text
**
	 * 하위 카테고리의 개수를 계산하는 기능
	 *
     * @param		inputData		String[][]		입력데이터(카테고리 정보)
     * @param		categoryStr		String			입력데이터(카테고리)
     * @return						int 			하위 카테고리의 개수
	 */
	public int getNumberOfSubcategories(String[][] inputData, String categoryStr) {
		int numberOfSubcategories = 0;
		////////////////////////여기부터 구현 (2) ---------------->
		Map<String, List<String>> tMap = makeMap(inputData);
		System.out.println(tMap);
		Queue<String> cnt = new LinkedList<>();

		String parent = getParent(tMap, categoryStr);
		List<String> values = tMap.get(parent);
							
		for (String v1 : values) {
			cnt.offer(v1);
		}

		while (!cnt.isEmpty()) {
			String res = cnt.poll();
			numberOfSubcategories++;

			if (tMap.containsKey(res)) {
				values = tMap.get(res);

				for (String v1 : values) {
					cnt.offer(v1);
				}
			}
		}

		///////////////////////////// <-------------- 여기까지 구현 (2)
		return numberOfSubcategories;
	}
	
	public String getParent(Map<String, List<String>> tMap, String child){
		String parent = "";
		
		for(String key:tMap.keySet()){
			List<String> values = tMap.get(key);
			if ( values.contains(child) ) {
				parent = key;
				break;
			}
		}
		
		return parent;
	}
	
	
	public List<String> getChlids(Map<String, List<String>> tMap, String parent){
		List<String> childs = new ArrayList<String>();
		
		if ( tMap.containsKey(parent) ) {
			childs = tMap.get(parent);
		}
		
		return childs;
	}
	
	
	private Map<String, List<String>> makeMap(String [][]inputData){
		Map<String, List<String>> tMap = new LinkedHashMap<String, List<String>>();
		
		for(int i=0;i<inputData.length;i++){
			String parent = inputData[i][0];
			String child = inputData[i][1];
			
			if ( tMap.containsKey(parent) ) {
				List<String> childs = tMap.get(parent);
				childs.add(child);
				
				tMap.put(parent, childs);
			} else {
				List<String> childs = new ArrayList<String>();
				childs.add(child);
				
				tMap.put(parent, childs);
				
			}
		}
		return tMap;
	}
```

현재 빙산 지도에서 내부 물을 구분하는 기능

```text
public int[][] convertInnerWater(int[][] icebergMap) {

int[][] innerMap = null;

//////////////////////

innerMap = new int[icebergMap.length][icebergMap[0].length];
int rowCnt = icebergMap.length;
int colCnt = icebergMap[0].length;

// 처기화
for (int r = 0; r < icebergMap.length; r++) {
	for (int c = 0; c < icebergMap[r].length; c++) {
		innerMap[r][c] = icebergMap[r][c];
		if (r == 0 || c == 0 || r == icebergMap.length - 1 || c == icebergMap[r].length - 1) {
			if (icebergMap[r][c] == 0) {
				innerMap[r][c] = -1;
			}
		}
	}
}

for (int i = 0; i < Math.max(rowCnt, colCnt) - 1; i++) {
	checkOutWater(innerMap);
}

checkInnerWater(innerMap);
rollbackOutWater(innerMap);

/////////////////////////////

return innerMap;
}

private void checkOutWater(int[][] map) {
	for (int r = 0; r < map.length; r++) {
		for (int c = 0; c < map[r].length; c++) {
			if (map[r][c] == -1) {
				continue;
			} else if (map[r][c] == 0) {
				int[] around = getAround(map, r, c);
				for (int a : around) {
					if (a == -1) {
						map[r][c] = -1;
						break;
					}
				}
			}
		}
	}
}

private int[] getAround(int[][] map, int row, int col) {
	int up = -9;
	int right = -9;
	int down = -9;
	int left = -9;

	if (row != 0) {
		up = map[row - 1][col];
	}
	if (col != 0) {
		left = map[row][col - 1];
	}
	if (row != map.length - 1) {
		down = map[row + 1][col];
	}
	if (col != map[0].length - 1) {
		right = map[row][col + 1];
	}

	return new int[] { up, right, down, left };
}

private void checkInnerWater(int[][] innerMap) {
	for (int r = 0; r < innerMap.length; r++) {
		for (int c = 0; c < innerMap[r].length; c++) {
			if (innerMap[r][c] == 0) {
				innerMap[r][c] = 9;
			}
		}
	}
}

private void rollbackOutWater(int[][] innerMap) {
	for (int r = 0; r < innerMap.length; r++) {
		for (int c = 0; c < innerMap[r].length; c++) {
			if (innerMap[r][c] == -1) {
				innerMap[r][c] = 0;
			}
		}
	}

}

몇 년 후 빙산이 모두 사라지는지 구하는 기능
public int getCollapseYear(int[][] icebergMap) {

int collYear = 0;

//////////////////////

int[][] map = convertInnerWater(icebergMap);

while (hasIce(map)) {
	collYear++;
	map = warm(map);
	map = convertInnerWater(map);
	printMap(map, collYear);
}

/////////////////////////////

return collYear;
}

/**
* 빙하를 녹인다.
* 
* @param map
*/
private int[][] warm(int[][] map) {

int[][] innerMap = new int[map.length][map[0].length];

// 처기화
for (int r = 0; r < map.length; r++) {
	for (int c = 0; c < map[r].length; c++) {
		innerMap[r][c] = map[r][c];
	}
}

for (int r = 0; r < map.length; r++) {
	for (int c = 0; c < map[r].length; c++) {
		int val = map[r][c];

		if (val >= 1 && val <= 4) {
			int[] around = getAround(map, r, c);
			int outWaterCount = 0;
			for (int a : around) {
				if (a == 0) {
					outWaterCount++;
				}
			}
			if (outWaterCount == 1) {
				innerMap[r][c] = Math.max(0, val - 1);
			} else if (outWaterCount == 2) {
				innerMap[r][c] = Math.max(0, val - 2);
			} else if (outWaterCount == 3) {
				innerMap[r][c] = Math.max(0, val - 3);
			} else if (outWaterCount == 4) {
				innerMap[r][c] = Math.max(0, val - 4);
			}
		}

	}
}
for (int r = 0; r < innerMap.length; r++) {
	for (int c = 0; c < innerMap[r].length; c++) {
		if (innerMap[r][c]==9) {
			innerMap[r][c] = 0;
		}
	}
}

return innerMap;

}

private boolean hasIce(int[][] map) {
for (int r = 0; r < map.length; r++) {
	for (int c = 0; c < map[r].length; c++) {
		if (map[r][c] != 0) {
			return true;
		}
	}
}
return false;
}

private static boolean DEBUG = false;

private void printMap(int[][] map, int year) {

debug("============================" + year);
for (int r = 0; r < map.length; r++) {
	String line = "";
	for (int c = 0; c < map[r].length; c++) {
		line += (map[r][c] + " ");
	}
	debug(line);
}
debug("============================" + year);
}

private static void debug(Object obj) {
if (DEBUG) {
	System.out.println(obj);
}
}
```



건물간 이동시간
```text
/**
 * 셔틀을 타지 않고 출발지에서 도착지까지 최소 이동하는 시간(초)을 구하는 기능
 * 
 * @param 		bicycleStation		자전거 보관소가 있는 건물 목록
 * @param 		start				출발지
 * @param 		destination			도착지
 * @return		int					셔틀을 타지 않고 최소 이동 시간
 */
public int getTraveltimeWithoutShuttle( String[] bicycleStation, String start, String destination ) {

	int traveltime = 0;

	////////////////////////여기부터 코딩 (1) ---------------->

	int startLoc = Integer.parseInt(start.substring(1));
	int endLoc = Integer.parseInt(destination.substring(1));
	traveltime = 240*Math.abs(endLoc - startLoc);

	//System.out.println("startLoc=E" + startLoc + " endLoc=E" + endLoc + " walkTime=" + traveltime);

	int bicStartLoc = startLoc;
	int startTime = Integer.MAX_VALUE;

	for(int i=0; i < bicycleStation.length; i++) {
		int bicLoc = Integer.parseInt(bicycleStation[i].substring(1)); 
		int tempTime = 240*Math.abs(bicLoc - startLoc);
		if( startTime > tempTime) {
			startTime = tempTime;
			bicStartLoc = bicLoc;
		}
	}

	//System.out.println("startTime=" + startTime + " bicStartLoc=E" + bicStartLoc);

	for(int i=0; i < bicycleStation.length; i++) {
		int bicLoc = Integer.parseInt(bicycleStation[i].substring(1)); 
		if( bicLoc != startLoc) {
			int bicTime = 70*Math.abs(bicLoc - bicStartLoc) + 240*Math.abs(endLoc - bicLoc) + startTime;
			if( traveltime > bicTime) {
				traveltime = bicTime;
			}
		}
	}

	///////////////////////////// <-------------- 여기까지 코딩 (1)

	return traveltime;
}

/**
 * 셔틀 탑승이 가능할 때, 출발지에서 도착지까지 최소 이동 시간(초)을 구하는 기능
 * 
 * @param 		bicycleStation		자전거 보관소가 있는 건물 목록
 * @param 		start				출발지
 * @param 		destination			도착지
 * @param 		departure			출발 시각 (HH:MM 형태)
 * @return		int					최소 이동 시간
 */
public int getTraveltime( String[] bicycleStation, String start, String destination, String departure) {

	int traveltime = 0;

	////////////////////////여기부터 코딩 (2) ---------------->

	String[] token = departure.split(":");
	int currentHour = Integer.parseInt(token[0]);
	int currentMin = Integer.parseInt(token[1]);

	int startLoc = Integer.parseInt(start.substring(1));
	int endLoc = Integer.parseInt(destination.substring(1));
	traveltime = 240*Math.abs(endLoc - startLoc);

	//System.out.println("startLoc=E" + startLoc + " endLoc=E" + endLoc + " walkTime=" + traveltime );

	int toBusTime = 240*Math.min(Math.abs(1 - startLoc), Math.abs(12 - startLoc));
	int fromBusTime = 240*Math.min(Math.abs(1 - endLoc), Math.abs(12 - endLoc));

	int waitTime = 60*(10-(currentMin + (int)(toBusTime/60))%10);

	int busTime = 220 + toBusTime + fromBusTime + waitTime;

	//System.out.println("waitTime=" + waitTime + " toBusTime=" + toBusTime + " fromBusTime=" + fromBusTime + " busTime=" + busTime);

	traveltime = Math.min(busTime, traveltime);

	int bicStartLoc = startLoc;
	int startTime = Integer.MAX_VALUE;

	for(int i=0; i < bicycleStation.length; i++) {
		int bicLoc = Integer.parseInt(bicycleStation[i].substring(1)); 
		int tempTime = 240*Math.abs(bicLoc - startLoc);
		if( startTime > tempTime) {
			startTime = tempTime;
			bicStartLoc = bicLoc;
		}
	}

	//System.out.println("startTime=" + startTime + " bicStartLoc=E" + bicStartLoc);

	for(int i=0; i < bicycleStation.length; i++) {
		int bicLoc = Integer.parseInt(bicycleStation[i].substring(1)); 
		if( bicLoc != startLoc) {
			int bicTime = 70*Math.abs(bicLoc - bicStartLoc) + 240*Math.abs(endLoc - bicLoc) + startTime;
			if( traveltime > bicTime) {
				traveltime = bicTime;
			}
		}
	}		



	///////////////////////////// <-------------- 여기까지 코딩 (2)

	return traveltime;
}
```


삼각형 막대개수
```text
/**
 * N개의 삼각형을 만들기 위한 막대 개수를 구하는 기능
 *
* @param		inputData			int		입력데이터(삼각형 개수)
* @return							int		막대 개수
 */
public int getNumberOfStickForTriangle(int inputData) {
	int numberOfStickForTriangle = 0;
	////////////////////////여기부터 구현 (1) ---------------->
	numberOfStickForTriangle =  3 + ( inputData - 1) * 2;
	///////////////////////////// <-------------- 여기까지 구현 (1)
	return numberOfStickForTriangle;
}


/**
 * N층의 피라미드를 만들기 위한 막대 개수를 구하는 기능
 *
* @param		numberOfLayers			int		입력데이터(피라미드 층수)
* @return								int		막대 개수
 */
public int getNumberOfStickForPyramid(int numberOfLayers) {
	int numberOfStickForPyramid = 0;
	////////////////////////여기부터 구현 (2) ---------------->
	int tNumberOfLayers = numberOfLayers;
	int sum = 0;
	for(;tNumberOfLayers>0;tNumberOfLayers--){
		sum = sum + (3 + (((2*tNumberOfLayers) - 2 ) * 2)); 
	}

	int nSum = 0;
	while(numberOfLayers != 1 ) {
		nSum = nSum + (numberOfLayers-1);
		numberOfLayers = numberOfLayers -1;
	}

	numberOfStickForPyramid = sum - nSum;
	///////////////////////////// <-------------- 여기까지 구현 (2)
	return numberOfStickForPyramid;
}
```

데이터 복원
```text

/**
 * 데이터 1차 복원 기능
 *
* @param		inputData			String		입력데이터(원본 데이터)
* @param		backup				String		입력데이터(백업 데이터)
* @return							String		1차 복원된 데이터
 */
public String getFirstRecovery(String inputData, String backup) {
	String firstRecovery = "";
	for(int i = 0 ; i < inputData.length(); i++){
		char currentCh = inputData.charAt(i);
		char backupCh = backup.charAt(i);

		if(Character.isDigit(currentCh)){
			if(Character.isDigit(backupCh)){
//					currentCh = backupCh;
				firstRecovery += currentCh;
			} else {
				firstRecovery += backupCh;
			}
		} else {
			firstRecovery += currentCh;
		}
	}
	return firstRecovery;
}


/**
 * 데이터 2차 복원 기능
 *
* @param		firstRecovery		String		1차 복원된 데이터
* @param		netWork				String[]	입력데이터(네트워크에 저장된 데이터)
* @return							String		2차 복원된 데이터
 */
public String getSecondRecovery(String firstRecovery, String[] netWork) {
	String secondRecovery = "";
	String netWorkStr = "";
	for(int i = 0; i < netWork.length; i++){
		netWorkStr += netWork[i].trim();
	}
	secondRecovery = getFirstRecovery(firstRecovery, netWorkStr);
	return secondRecovery;
}
```

악성코드
```test
/**
 * 1단계 악성코드 제거
 * 
* @param		inputData				List		입력데이터(코드 문자열 목록)
* @return								List		1단계 악성코드가 제거된 문자열 목록
 */
public List<String> getFirstCode(List<String> inputData){
	List<String> firstCodeNameList = null;
	//////////////////////여기부터 구현 (1) ---------------->
	firstCodeNameList = new ArrayList<String>();
	for(String data:inputData){
		if ( data.indexOf(".") > -1 ) {
			firstCodeNameList.add(data);
		}
	}
	///////////////////////////// <-------------- 여기까지 구현 (1)
	return firstCodeNameList;
}

/**
 * 2단계 악성코드 제거
 * 
* @param		firstCodeNameList			List		1단계 악성코드가 제거된 문자열 목록
* @return									List		2단계 악성코드가 제거된 문자열 목록
 */
public List<String> getSecondCode(List<String> firstCodeNameList){
	List<String> secondCodeNameList = null;
	//////////////////////여기부터 구현 (2) ---------------->
	secondCodeNameList = new ArrayList<String>();
	for(String data:firstCodeNameList){
		String ext = data.substring(data.lastIndexOf("."));
		data = data.substring(0, data.lastIndexOf("."));

		boolean added = false;

		if ( data.indexOf("a") > -1 && data.indexOf("x") > -1 ) {
			if ( data.indexOf("ax") > -1 ) {
				secondCodeNameList.add(data+ext);
				added = true;
			}						
		} 

		if ( !added ) {
			if ( data.indexOf("a") > -1 || data.indexOf("x") > -1 ) {
				if ( data.indexOf("ab") > -1 || data.indexOf("xy") > -1 ) {
					secondCodeNameList.add(data+ext);
				}
			} else {
				secondCodeNameList.add(data+ext);
			}
		}
	}
	///////////////////////////// <-------------- 여기까지 구현 (2)
	return secondCodeNameList;
}
```

NxN 배열 최대합

```text
/**
 * 부분 배열의 개수를 구하는 기능
 *
* @param		arraySize			int		배열 크기
* @return							int		부분 배열의 개수
 */
public int getNumberOfSubArrays(int arraySize) {
	int numberOfSubArrays = 0;
	////////////////////////여기부터 구현 (1) ---------------->
	for(int i=1;i<=arraySize;i++){
		numberOfSubArrays += getNumberSum(arraySize, i);
	}

	///////////////////////////// <-------------- 여기까지 구현 (1)
	return numberOfSubArrays;
}


private int getNumberSum(int arraySize, int initialNumber) {
	int maxX = 0;

	for(int i=initialNumber;i<=arraySize;i++){
		if ( i <= arraySize ) {
			maxX++;
		} else {
			break;
		}

	}

	return (maxX * maxX);
}


/**
 * 최대값을 찾는 기능
 *
* @param		inputData			int[][]		입력데이터(NxN배열)
* @return							int			최대값
 */
public int getMaximumValue(int[][] inputData) {
	int maximumValue = -1;
	boolean bFirst = false;

	////////////////////////여기부터 구현 (2) ---------------->
	for(int i=1;i<=inputData.length;i++){
		int tMaximumValue = getMaxValue(inputData,i);

		if ( bFirst ) {
			bFirst = false;
			maximumValue = tMaximumValue;
		} else {
			if ( maximumValue < tMaximumValue ) {
				maximumValue = tMaximumValue;
			}
		}
	}

	///////////////////////////// <-------------- 여기까지 구현 (2)
	return maximumValue;
}


private int getMaxValue(int[][] inputData, int endValue) {
	int maximumValue = 0;
	int maxLength = inputData.length;
	int orgCurrentXEnd = endValue;

	int currentXEnd = endValue;
	int currentYEnd = endValue;
	int currentXStart = 0;
	int currentYStart = 0;

	while ( maxLength >= currentXEnd ) {
		int sum = 0;
		for(int i=currentXStart;i<currentXEnd;i++){
			for(int j=currentYStart;j<currentYEnd;j++){
				sum = sum + inputData[j][i];
			}
		}
		currentXStart++;;
		currentXEnd++;

		if ( maximumValue < sum ) {
			maximumValue = sum;
		}
	}
	currentYStart++;
	currentYEnd++;

	currentXEnd = orgCurrentXEnd;
	currentXStart = 0;
	while ( maxLength >= currentYEnd ) {
		int sum = 0;
		for(int i=currentXStart;i<currentXEnd;i++){
			for(int j=currentYStart;j<currentYEnd;j++){
				sum = sum + inputData[j][i];
			}
		}
		currentXStart++;;
		currentXEnd++;

		currentYStart++;
		currentYEnd++;

		if ( maximumValue < sum ) {
			maximumValue = sum;
		}
	}
	return maximumValue;
}
```

카테코리
```text
/**
 * 상위 카테고리를 검색하는 기능
 *
* @param		inputData		String[][]		입력데이터(카테고리 정보)
* @param		categories		List			입력데이터(inputCategories[0]: 카테고리1, inputCategories[1]: 카테고리2)
* @return						String 			상위 카테고리
 */
public String getTopCategory(String[][] inputData, List<String> categories) {
	String topCategory = "";
	////////////////////////여기부터 구현 (1) ---------------->
	Map<String, List<String>> tMap = new LinkedHashMap<String, List<String>>();

	for(int i=0;i<inputData.length;i++){
		String parent = inputData[i][0];
		String child = inputData[i][1];

		if ( tMap.containsKey(parent) ) {
			List<String> childs = tMap.get(parent);
			childs.add(child);

			tMap.put(parent, childs);
		} else {
			List<String> childs = new ArrayList<String>();
			childs.add(child);

			tMap.put(parent, childs);

		}
	}

	List<String> hierarchy = new ArrayList<String>();

	int index = -1;

	boolean bFirst = false;

	for(String inputCategory:categories){
		if ( !bFirst ) {
			for(String key:tMap.keySet()){
				List<String> values = tMap.get(key);
				if ( values.contains(inputCategory) ) {
					hierarchy.add(key);

					String parent = getParent(tMap, key);
					while(!parent.isEmpty()){
						hierarchy.add(0, parent);
						parent = getParent(tMap, parent);
					}

					break;
				}
			}
			bFirst = true;
		} else {
			for(String key:tMap.keySet()){
				List<String> values = tMap.get(key);
				if ( values.contains(inputCategory) ) {
					List<String> tHierarchy = new ArrayList<String>();

					tHierarchy.add(key);

					String parent = getParent(tMap, key);
					while(!parent.isEmpty()){
						tHierarchy.add(0, parent);
						parent = getParent(tMap, parent);
					}

					for(String tParent:tHierarchy){
						for(int i=0;i<hierarchy.size();i++){
							String oParent = hierarchy.get(i);
							if ( oParent.equals(tParent) ) {
								if ( index < i ) {
									index = i;
								}
								break;
							}
						}
					}

					break;
				}
			}
		}
	}

	if ( index > -1 ) {
		topCategory = hierarchy.get(index);
	}

	///////////////////////////// <-------------- 여기까지 구현 (1)
	return topCategory;
}

public String getParent(Map<String, List<String>> tMap, String child){
	String parent = "";

	for(String key:tMap.keySet()){
		List<String> values = tMap.get(key);
		if ( values.contains(child) ) {
			parent = key;
			break;
		}
	}

	return parent;
}

public List<String> getChlids(Map<String, List<String>> tMap, String parent){
	List<String> childs = new ArrayList<String>();

	if ( tMap.containsKey(parent) ) {
		childs = tMap.get(parent);
	}

	return childs;
}


/**
 * 하위 카테고리의 개수를 계산하는 기능
 *
* @param		inputData		String[][]		입력데이터(카테고리 정보)
* @param		categoryStr		String			입력데이터(카테고리)
* @return						int 			하위 카테고리의 개수
 */
public int getNumberOfSubcategories(String[][] inputData, String categoryStr) {
	int numberOfSubcategories = 0;
	////////////////////////여기부터 구현 (2) ---------------->
	Map<String, List<String>> tMap = new LinkedHashMap<String, List<String>>();

	for(int i=0;i<inputData.length;i++){
		String parent = inputData[i][0];
		String child = inputData[i][1];

		if ( tMap.containsKey(parent) ) {
			List<String> childs = tMap.get(parent);
			childs.add(child);

			tMap.put(parent, childs);
		} else {
			List<String> childs = new ArrayList<String>();
			childs.add(child);

			tMap.put(parent, childs);

		}
	}
	for(String key:tMap.keySet()){
		List<String> values = tMap.get(key);
		if ( values.contains(categoryStr) ) {

			String parent = getParent(tMap, categoryStr);

			List<String> children = new ArrayList<String>();
			getChildren(tMap, parent, children);

			numberOfSubcategories = children.size();

			break;
		}
	}
	///////////////////////////// <-------------- 여기까지 구현 (2)
	return numberOfSubcategories;
}

private void getChildren(Map<String, List<String>> tMap, String parent, List<String> children) {
	new ArrayList<String>();

	// 상위 카테고리..
	List<String> tChildren = getChlids(tMap, parent);
	if (tChildren.size() >  0 ) {
		children.addAll(tChildren);

		for(String tChildParents:tChildren){
			getChildren(tMap, tChildParents, children);
		}
	}
}
```
