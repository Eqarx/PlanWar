#include<iostream>
#include<windows.h>
#include<conio.h>
#include<time.h>
#include<string>
using namespace std;

//��ܽṹ�����磺�з��ɻ������ֵ� 
typedef struct Frame
{
    COORD position[2];
    int flag;
}Frame;

//���������COORD��x��y 
void SetPos(COORD a)
{
    HANDLE out = GetStdHandle(STD_OUTPUT_HANDLE);
    SetConsoleCursorPosition(out, a);
}

// ���ú������� x��y 
void SetPos(int i, int j)
{
    COORD pos = { i, j };
    SetPos(pos);
}
//���ع�� 
void HideCursor()
{
    CONSOLE_CURSOR_INFO cursor_info = { 1, 0 };
    SetConsoleCursorInfo(GetStdHandle(STD_OUTPUT_HANDLE), &cursor_info);
}

/*��������*/ 
//����� 
void drawRow(int m, int n1, int n2, char ch)
{
    SetPos(n1, m);
    for (int i = 0; i <= (n2 - n1); i++)
        cout << ch;
}
//��a, b ��������ͬ��ǰ���£������� [a, b] ֮�����Ϊ ch
void drawRow(COORD a, COORD b, char ch)
{
    if (a.Y == b.Y)
        drawRow(a.Y, a.X, b.X, ch);
    else
    {
        SetPos(0, 25);
        cout << "error code 01���޷�����У���Ϊ���������������(x)�����";
        system("pause");
    }
}

//�ѵ�x�У�[y1, y2] ֮����������Ϊ ch
void drawCol(int x, int y1, int y2, char ch)
{
    int y = y1;
    while (y != y2 + 1)
    {
        SetPos(x, y);
        cout << ch;
        y++;
    }
}
//��a, b ��������ͬ��ǰ���£������� [a, b] ֮�����Ϊ ch
void drawCol(COORD a, COORD b, char ch)
{
    if (a.X == b.X)
        drawCol(a.X, a.Y, b.Y, ch);
    else
    {
        SetPos(0, 25);
        cout << "error code 02���޷�����У���Ϊ��������ĺ�����(y)�����";
        system("pause");
    }
}

/*����Ӧ���󣺷ɻ����л����ӵ�*/ 
//���Ͻ����ꡢ���½����ꡢ��row����С���col�����
//���� 
void drawFrame(COORD a, COORD  b, char row, char col)
{
    drawRow(a.Y, a.X + 1, b.X - 1, row);
    drawRow(b.Y, a.X + 1, b.X - 1, row);
    drawCol(a.X, a.Y + 1, b.Y - 1, col);
    drawCol(b.X, a.Y + 1, b.Y - 1, col);
}
void drawFrame(int x1, int y1, int x2, int y2, char row, char col)
{
    COORD a = { x1, y1 };
    COORD b = { x2, y2 };
    drawFrame(a, b, row, col);
}
void drawFrame(Frame frame, char row, char col)
{
    COORD a = frame.position[0];
    COORD b = frame.position[1];
    drawFrame(a, b, row, col);
}

//��Ϸ������� 
void drawPlaying()
{
    drawFrame(0, 0, 48, 24, '=', '|');//   draw map frame;
    drawFrame(49, 0, 79, 4, '-', '|');//       draw output frame
    drawFrame(49, 4, 79, 9, '-', '|');//       draw score frame
    drawFrame(49, 9, 79, 20, '-', '|');//  draw operate frame
    drawFrame(49, 20, 79, 24, '-', '|');// draw other message frame
    SetPos(52, 6);
    cout << "�÷֣�";
    SetPos(52, 7);
    cout << "�ƺţ�";
    SetPos(52, 10);
    cout << "������ʽ��";
    SetPos(52, 12);
    cout << "  a,s,d,w ����ս���ƶ���";
    SetPos(52, 14);
    cout << "  p ��ͣ��Ϸ��";
    SetPos(52, 16);
    cout << "  e �˳���Ϸ��";
}

//��[a, b)֮�����һ���������
int random(int a, int b)
{
    int c = (rand() % (a - b)) + a;
    return c;
}
//��������������ľ��ο����������һ������
COORD random(COORD a, COORD b)
{
    int x = random(a.X, b.X);
    int y = random(a.Y, b.Y);
    COORD c = { x, y };
    return c;
}

//�ж�����frame�����Ƿ���ײ 
bool  judgeCoordInFrame(Frame frame, COORD spot)
{
    if (spot.X >= frame.position[0].X)
        if (spot.X <= frame.position[1].X)
            if (spot.Y >= frame.position[0].Y)
                if (spot.Y <= frame.position[0].Y)
                    return true;
    return false;
}

//��ӡ���� 
void printCoord(COORD a)
{
    cout << "( " << a.X << " , " << a.Y << " )";
} 
void printFrameCoord(Frame a)
{
    printCoord(a.position[0]);
    cout << " - ";
    printCoord(a.position[1]);
}

//��Ϸ��½������� 
int drawMenu()
{
    SetPos(30, 1);
    cout << "�ɻ���ս-������";
    drawRow(3, 0, 79, '-');
    drawRow(5, 0, 79, '-');
    SetPos(28, 4);
    cout << "w �� s ѡ�� k ȷ��";
    SetPos(15, 11);
    cout << "1. Easy Mode";
    SetPos(15, 13);
    cout << "2. Hard Mode";
    drawRow(20, 0, 79, '-');
    drawRow(22, 0, 79, '-');
    SetPos(47, 11);
    cout << "�������ԣ�";
    SetPos(51, 13);
    cout << "���Ž������ƶ��ٶȡ�";
    SetPos(24, 21);
    int j = 11;
    SetPos(12, j);
    cout << ">>";

    while (1)
    {
        if (_kbhit())
        {
            char x = _getch();
            switch (x)
            {
            case 'w':
            {
                if (j == 13)
                {
                    SetPos(12, j);
                    cout << "��";
                    j = 11;
                    SetPos(12, j);
                    cout << ">>";
                    SetPos(51, 13);
                    cout << "������������������������";
                    SetPos(47, 11);
                    cout << "�������ԣ�";
                    SetPos(51, 13);
                    cout << "���Ž������ƶ��ٶȡ�";
                }
                break;
            }
            case 's':
            {
                if (j == 11)
                {
                    SetPos(12, j);
                    cout << "��";
                    j = 13;
                    SetPos(12, j);
                    cout << ">>";
                    SetPos(51, 13);
                    cout << "����������������������������";
                    SetPos(47, 11);
                    cout << "�������ԣ�";
                    SetPos(51, 13);
                    cout << "�ƶ��ٶȽϿ졣";
                }
                break;
            }
            case 'k':
            {
                if (j == 8)  return 1;
                else return 2;
            }
            }
        }
    }
}

/*��Ϸ��*/
class Game
{
public:
    COORD position[10]; //�ɻ��������� 
    COORD bullet[10]; //�ӵ� 
    Frame enemy[8];  //�з��ɻ�������� 
    int score;  //�÷� 
    int rank;   //���� 
    int rankf;
    string title;
    int flag_rank;

    Game();

    //��ʼ������
    void initPlane();
    void initBullet();
    void initEnemy();

    //��ʼ������һ��
    //void initThisBullet( COORD );
    //void initThisEnemy( Frame );

    void planeMove(char);
    void bulletMove();
    void enemyMove();

    //�������
    void drawPlane();
    void drawPlaneToNull();
    void drawBullet();
    void drawBulletToNull();
    void drawEnemy();
    void drawEnemyToNull();

    //�������һ��
    void drawThisBulletToNull(COORD);
    void drawThisEnemyToNull(Frame);

    void Pause();
    void Playing();
    void judgePlane();
    void judgeEnemy();

    void Shoot();

    void GameOver();
    void printScore();
};

Game::Game()
{
    initPlane();
    initBullet();
    initEnemy();
    score = 0;
    rank = 25;
    rankf = 0;
    flag_rank = 0;
}

//�ɻ���ʼ��-------------------- 
void Game::initPlane()
{
    COORD centren = { 39, 22 };
    position[0].X = position[6].X = centren.X;
    position[1].X = centren.X - 2;
    position[2].X = position[5].X = position[8].X = centren.X - 1;
    position[3].X = position[7].X = position[9].X = centren.X + 1;
    position[4].X = centren.X + 2;
    for (int i = 0; i <= 4; i++)
        position[i].Y = centren.Y;
    for (int i = 5; i <= 7; i++)
        position[i].Y = centren.Y - 1;
    position[8].Y = centren.Y + 1;
    position[9].Y = centren.Y + 1;

}
//���ɻ� 
void Game::drawPlane()
{
    for (int i = 0; i < 10; i++)
    {
        SetPos(position[i]);
        if (i == 0 || i== 8 || i==9)
            cout << "*";
        else if (i == 5)
            cout << "/";
        else if (i == 6)
            cout << "=";
        else if (i == 7)
            cout << "\\";
        else if (i == 1 || i== 2)
            cout << "<";
        else if (i == 3 || i== 4)
            cout << ">";
    }
}
//�ɻ���� 
void Game::drawPlaneToNull()
{
    for (int i = 0; i < 10; i++)
    {
        SetPos(position[i]);
        cout << " ";
    }
}

//�ӵ���ʼ�� 
void Game::initBullet()
{
    for (int i = 0; i < 10; i++)
        bullet[i].Y = 30;
}
//���ӵ� 
void Game::drawBullet()
{
    for (int i = 0; i < 10; i++)
    {
        if (bullet[i].Y != 30)
        {
            SetPos(bullet[i]);
            cout << "^";
        }
    }
}
//�ӵ���� 
void Game::drawBulletToNull()
{
    for (int i = 0; i < 10; i++)
        if (bullet[i].Y != 30)
        {
            COORD pos = { bullet[i].X, bullet[i].Y + 1 };
            SetPos(pos);
            cout << " ";
        }
}

//��ʼ���л� 
void Game::initEnemy()
{
    COORD a = { 1, 1 };
    COORD b = { 45, 15 };
    for (int i = 0; i < 8; i++)
    {
        enemy[i].position[0] = random(a, b);
		enemy[i].position[1].X = enemy[i].position[0].X + 2;
        enemy[i].position[1].Y = enemy[i].position[0].Y + 1;
    }

}
//���л� 
void Game::drawEnemy()
{
    for (int i = 0; i < 8; i++){
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X, enemy[i].position[0].X, '\\');
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X+1, enemy[i].position[0].X+1, '+');
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X+2, enemy[i].position[0].X+2, '/');
		drawRow(enemy[i].position[0].Y+1, enemy[i].position[0].X+1, enemy[i].position[0].X+1, '|');
		}
}
//�л���� 
void Game::drawEnemyToNull()
{
    for (int i = 0; i < 8; i++)
    {
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X, enemy[i].position[0].X, ' ');
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X+1, enemy[i].position[0].X+1, ' ');
		drawRow(enemy[i].position[0].Y, enemy[i].position[0].X+2, enemy[i].position[0].X+2, ' ');
		drawRow(enemy[i].position[0].Y+1, enemy[i].position[0].X+1, enemy[i].position[0].X+1, ' ');	
    }
}

//��Ϸ��ͣ 
void Game::Pause()
{
    SetPos(61, 2);
    cout << "               ";
    SetPos(61, 2);
    cout << "��ͣ��...";
    char c = _getch();
    while (c != 'p')
        c = _getch();
    SetPos(61, 2);
    cout << "         ";
}

//�ƶ��ɻ� 
void Game::planeMove(char x)
{
    if (x == 'a')
        if (position[1].X != 1)
            for (int i = 0; i <= 9; i++)
                position[i].X -= 2;

    if (x == 's')
        if (position[7].Y != 23)
            for (int i = 0; i <= 9; i++)
                position[i].Y += 1;

    if (x == 'd')
        if (position[4].X != 47)
            for (int i = 0; i <= 9; i++)
                position[i].X += 2;

    if (x == 'w')
        if (position[5].Y != 3)
            for (int i = 0; i <= 9; i++)
                position[i].Y -= 1;
}

//�ӵ��ƶ� 
void Game::bulletMove()
{
    for (int i = 0; i < 10; i++)
    {
        if (bullet[i].Y != 30)
        {
            bullet[i].Y -= 1;
            if (bullet[i].Y == 1)
            {
                COORD pos = { bullet[i].X, bullet[i].Y + 1 };
                drawThisBulletToNull(pos);
                bullet[i].Y = 30;
            }

        }
    }
}

//�л��ƶ� 
void Game::enemyMove()
{
    for (int i = 0; i < 8; i++)
    {
        for (int j = 0; j < 2; j++)
            enemy[i].position[j].Y++;

        if (24 == enemy[i].position[1].Y)
        {
        	//�ɻ��ɳ����棬�۷� 
        	score -= 1; 
            COORD a = { 1, 1 };
            COORD b = { 45, 3 };
            enemy[i].position[0] = random(a, b);
            enemy[i].position[1].X = enemy[i].position[0].X + 2;
            enemy[i].position[1].Y = enemy[i].position[0].Y + 1;
        }
    }
}

//�ɻ��о���׹���ж� 
void Game::judgePlane()
{
    for (int i = 0; i < 8; i++)
        for (int j = 0; j < 9; j++)
            if (judgeCoordInFrame(enemy[i], position[j]))
            {
                SetPos(62, 1);
                cout << "׹��";
                drawFrame(enemy[i], '+', '+');
                Sleep(1000);
                GameOver();
                break;
            }
}

void Game::drawThisBulletToNull(COORD c)
{
    SetPos(c);
    cout << " ";
}

void Game::drawThisEnemyToNull(Frame f)
{
//    drawFrame(f, ' ', ' ');
	drawRow(f.position[0].Y, f.position[0].X, f.position[0].X, ' ');
	drawRow(f.position[0].Y, f.position[0].X+1, f.position[0].X+1, ' ');
	drawRow(f.position[0].Y, f.position[0].X+2, f.position[0].X+2, ' ');
	drawRow(f.position[0].Y+1, f.position[0].X+1, f.position[0].X+1, ' ');	
}

// �л��о������мӷ� 
void Game::judgeEnemy()
{
    for (int i = 0; i < 8; i++)
        for (int j = 0; j < 10; j++)
            if (judgeCoordInFrame(enemy[i], bullet[j]))
            {
            	//���У��ӷ� 
                score += 1;
                drawThisEnemyToNull(enemy[i]);
                COORD a = { 1, 1 };
                COORD b = { 45, 3 };
                enemy[i].position[0] = random(a, b);
                enemy[i].position[1].X = enemy[i].position[0].X + 2;
                enemy[i].position[1].Y = enemy[i].position[0].Y + 1;
                drawThisBulletToNull(bullet[j]);
                bullet[j].Y = 30;
            }
}

//��� 
void Game::Shoot()
{
    for (int i = 0; i < 10; i++)
        if (bullet[i].Y == 30)
        {
            bullet[i].X = position[5].X;
            bullet[i].Y = position[5].Y - 1;
            break;
        }
}

//��ӡ�÷� ���÷ֵȼ����� 
void Game::printScore()
{
    if (score == 10 && flag_rank == 0)
    {
        rank -= 3;
        flag_rank = 1;
    }

    else if (score == 25 && flag_rank == 1)
    {
        rank -= 5;
        flag_rank = 2;
    }
    else if (score == 50 && flag_rank == 2)
    {
        rank -= 5;
        flag_rank = 3;
    }
    int x = rank / 5;
    SetPos(60, 6);
    cout << score;

    if (rank != rankf)
    {
        SetPos(60, 7);
        if (x == 5)
            title = "��������Ա";
        else if (x == 4)
            title = "�м�����Ա";
        else if (x == 3)
            title = "�߼�����Ա";
        else if (x == 2)
            title = "���Ʒ���Ա";
        cout << title;
    }
    rankf = rank;
}

//��Ϸ���� 
void Game::Playing()
{
    //HANDLE MFUN;
    //MFUN= CreateThread(NULL, 0, MusicFun, NULL, 0, NULL); 

    drawEnemy();
    drawPlane();

    int flag_bullet = 0;
    int flag_enemy = 0;

    while (1)
    {
        Sleep(8);
        if (_kbhit())
        {
            char x = _getch();
            if ('a' == x || 's' == x || 'd' == x || 'w' == x)
            {
                drawPlaneToNull();
                planeMove(x);
                drawPlane();
                judgePlane();
            }
            else if ('p' == x)
                Pause();
            else if ('k' == x)
                Shoot();
            else if ('e' == x)
            {
                //CloseHandle(MFUN);
                GameOver();
                break;
            }

        }
        /* �����ӵ� */
        if (0 == flag_bullet)
        {
            bulletMove();
            drawBulletToNull();
            drawBullet();
            judgeEnemy();
        }
        flag_bullet++;
        if (5 == flag_bullet)
            flag_bullet = 0;

        /* �������� */
        if (0 == flag_enemy)
        {
            drawEnemyToNull();
            enemyMove();
            drawEnemy();
            judgePlane();
        }
        flag_enemy++;
        if (flag_enemy >= rank)
            flag_enemy = 0;
        /*����Ϊ0����Ϸ����*/ 
        if (score < 0)
            {
                SetPos(62, 1);
                cout << "��������";
                Sleep(1000);
                score = 0;
                GameOver();
                break;
            }

        /* ����÷� */
        printScore();
    }
}

//��Ϸ���� 
void Game::GameOver()
{
    system("cls");
    COORD p1 = { 28,9 };
    COORD p2 = { 53,15 };
    drawFrame(p1, p2, '=', '|');
    SetPos(36, 12);
    string str = "Game Over!";
    for (int i = 0; i < str.size(); i++)
    {
        Sleep(80);
        cout << str[i];
    }
    Sleep(1000);
    system("cls");
    drawFrame(p1, p2, '=', '|');
    //SetPos(31, 11);
    //cout << "����л���" << score / 5 << " ��";
    SetPos(31, 11);
    cout << "�á����֣�" << score;
    SetPos(31, 12);
    cout << "��óƺţ�" << title;
    SetPos(30, 16);
    Sleep(1000);
    cout << "������ �ǣ�y��| ��n��";
as:
    char x = _getch();
    if (x == 'n')
        exit(0);
    else if (x == 'y')
    {
        system("cls");
        Game game;
        int a = drawMenu();
        if (a == 2)
            game.rank = 25;
        system("cls");
        drawPlaying();
        game.Playing();
    }
    else goto as;
}

/*================== the main function ==================*/
int main()
{
    //��Ϸ׼��
    srand((int)time(0));    //�������
    HideCursor();   //���ع��

    Game game;
    int a = drawMenu();
    if (a == 2)
        game.rank = 25;
    system("cls");
    drawPlaying();
    game.Playing();
}
