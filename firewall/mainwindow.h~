#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QMessageBox>
#include <QVector>
#include <QTimer>
#include <QFile>
#include <QFileInfo>
#include <QTextStream>
#include <QDebug>

/* ioctr commands */
#define FW_ADD_RULE 0
#define FW_DEL_RULE 1
#define FW_CLEAR_RULE 12

#define FW_GET_NAT_LEN 3
#define FW_REFRESH_NAT_RULE 4
#define FW_START_NAT_TRANSFORM 5
#define FW_STOP_NAT_TRANSFORM 6
#define FW_GET_ACTIVELINK_LEN 7
#define FW_REFRESH_ACTIVELINK 8
#define FW_GET_LOG_LEN 9
#define FW_WRITE_LOG 10

/* some limit conditions */
#define MAX_RECORD 256   // max record number
#define MIN_PORT 0
#define MAX_PORT 0xFFFF

class mtime{
public:
    int year;
    int month;
    int day;
    int hour;
    int min;
    int sec;
};

class Host{
public:
    u_int32_t ip;
    u_int16_t mask;
    u_int32_t natip;
};

class Node{
public:
  unsigned int sip;
  unsigned int dip;
  unsigned short sport;
  unsigned short dport;
  unsigned short protocol;
  unsigned short sMask;
  unsigned short dMask;
  bool isPermit;
  bool isLog;
  struct Node *next;          //单链表的指针域
};

class Nat{
public:
    unsigned int ip;
    unsigned int natip;
    unsigned short port;
    unsigned short natport;
    struct Nat *next;
};

class State{
public:
    unsigned int sip;
    unsigned int dip;
    unsigned short sport;
    unsigned short dport;
    u_int8_t protocol;
    mtime createtime;
    u_int8_t lifetime;
    bool log;
    struct State *next;
};

struct Log{
    u_int32_t sip;
    u_int32_t dip;
    u_int16_t sport;
    u_int16_t dport;
    u_int8_t protocol;
    mtime time;
    bool accept;
    Log *next;
};

namespace Ui {
class MainWindow;
}

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    explicit MainWindow(QWidget *parent = 0);
    ~MainWindow();

private slots:
    void addRulestoList();
    void deleteOneItem();
    void clearRuleList();
    void startNat();
    void stopNat();

    void update_InfoFromDevice();

private:
    Ui::MainWindow *ui;
    QVector<Node> ruleList;
    QVector<Nat> natList;

    QTimer *timer;

    int fd;

    unsigned int inet_addr(char *str);

    void addARuleToTable(Node item,unsigned int i);
    QString get_string_ip_addr(unsigned int ip);
    QString getProtocolName(unsigned short protocolNumber);
    unsigned short getProtocolNumber(QString protocol);
    bool check_ip(QString ipstr);
    bool check_port(QString portStr);
    unsigned short get_port(QString portStr);
    unsigned short get_subnet_mask_number(QString ipstr);

    void addStateToTable(const State &item);

    void writelog(const Log *item,int len);

    void addNatToTable(const Nat &item);

};

#endif // MAINWINDOW_H
