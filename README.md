카카오 프렌즈 컬러링북

#include <vector>
#include <algorithm>

using namespace std;

void CountColor(vector<vector<int>>& picture, int x, int y, int& cnt) {
    int color = picture[x][y];
    cnt++;
    picture[x][y] = 0;
    size_t xx, yy;
    vector<int> dx = { 1, -1, 0, 0 };
    vector<int> dy = { 0, 0, 1, -1 };
    for (int i = 0; i < 4; i++) {
        xx = x + dx[i];
        yy = y + dy[i];
        if (xx < picture.size() && yy < picture[0].size() && picture[xx][yy] == color)
            CountColor(picture, xx, yy, cnt);
    }

}

vector<int> solution(int m, int n, vector<vector<int>> picture) {
    vector<int> list;
    int cnt;
    for (int x = 0; x < picture.size(); x++)
        for (int y = 0; y < picture[0].size(); y++)
            if (picture[x][y] != 0) {
                cnt = 0;
                CountColor(picture, x, y, cnt);
                list.push_back(cnt);
            }
    return { (int)list.size(),  *max_element(list.begin(), list.end()) };
}
